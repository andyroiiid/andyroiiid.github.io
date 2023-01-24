---
title:  "Integrating glslang for runtime shader compilation"
date:   2023-01-14 18:00:00 -0600
categories: vulkan
tags: glslang
toc: true
---

In [my Vulkan engine](/personal_projects/haru-v/#glslang-runtime-shader-compilation), I needed a tool to compile GLSL into SPIR-V at runtime, so here's a tutorial of how I did it with `glslang`.

The official `glslang` standalone program [source](https://github.com/KhronosGroup/glslang/blob/master/StandAlone/StandAlone.cpp) is a great resource for integrating `glslang`.
{: .notice--info}

## Intializing and finalizing `glslang`

First, you need to include `ShaderLang.h`:

```c++
#include <glslang/Public/ShaderLang.h>
```

To intialize `glslang`, you can simply call `glslang::IntializeProcess()`. It needs to be called exactly once per process before using anything else.

```c++
void Initialize() {
    // ...
    glslang::InitializeProcess();
    // ...
}
```

To finalize `glslang`, you need to call `glslang::FinalizeProcess()`.

```c++
void Finalize() {
    // ...
    glslang::FinalizeProcess();
    // ...
}
```

You can also use `glslang::GetGlslVersionString()` to get `glslang` supported GLSL version.

```c++
void Intialize() {
    // ...
    printf("glslang GLSL version: %s", glslang::GetGlslVersionString());
    // ...
}
```

## Compiling GLSL Shaders

### Create a `glslang::TShader` object

To compile GLSL shaders, you need a `glslang::TShader` object and specify which stage the shader belongs to.

```c++
std::vector<uint32_t> CompileGLSLToSPRIV(const std::string &source) {
    const EShLanguage stage = EShLangVertex;
    // or EShLangFragment, EShLangGeometry, EShLangCompute, etc.

    glslang::TShader shader(stage);
    
    // ...
}
```

### Feeding shader source code

After creating the shader object, you can set source strings and `preamble`.

`preamble` is added to the front of the shader source, but it doesn't work the same as string concatenation (putting `#version` directive in `preamble` doesn't work). I usually use it for enabling extensions like `#extension GL_GOOGLE_include_directive : require`.

```c++
std::vector<uint32_t> CompileGLSLToSPRIV(const std::string &source) {
    // ...

    glslang::TShader shader(stage);

    shader.setStrings(source.c_str(), 1);
    shader.setPreamble("#extension GL_GOOGLE_include_directive : require\n");

    // ...
}
```

`ARB_shading_language_include` and `GL_GOOGLE_include_directive` are two **different** extensions, and `ARB_shading_language_include` doesn't work for `glslang`.
{: .notice--warning}

### Setting input and output settings

Then you need to pass in three settings: `EnvInput`, `EnvClient`, and `EnvTarget`.

According to the comments in `ShaderLang.h`, these three settings represent:

- `setEnvInput(EShSource langguageFamily, EShLanguage stage, EShClient dialect, int dialectVersion)`: The input source language and stage.
- `setEnvClient(EShClient client, EShTargetClientVersion version)`: The client APi and its version.
- `setEnvTarget(EShTargetLanguage lang, EShTargetLanguageVersion version)`: The target language and its version. Currently `lang` only supports `EShTargetSpv` for SPIR-V.

For example, I have a **vertex** shader source written in **GLSL**, and I'm using the **Vulkan** dialect of GLSL and version **100** of `GL_KHR_vulkan_glsl` extension.

I want to compile for **Vulkan**, and my Vulkan version is **1.3**. I want it to produce **SPIR-V** binaries, and I want SPIR-V **1.0** (the latest version is 1.6 but I want better compatibility).

So I would continue with:

```c++
std::vector<uint32_t> CompileGLSLToSPRIV(const std::string &source) {
    // ...

    shader.setEnvInput(glslang::EShSourceGlsl, EShLangVertex, glslang::EShClientVulkan, 100);
    shader.setEnvClient(glslang::EShClientVulkan, glslang::EShTargetVulkan_1_3);
    shader.setEnvTarget(glslang::EshTargetSpv, glslang::EShTargetSpv_1_0);

    // ...
}
```

### Parsing and linking the shader

For parsing shader, we need to specify a `TBulitInResource` to tell `glslang` how many resources the shader is allowed to use. This can be a SUPER long list (check [ResourceLimits.cpp](https://github.com/KhronosGroup/glslang/blob/master/StandAlone/ResourceLimits.cpp)), but luckily we can simply use the default config.

Here's how to parse the shader:

```c++
// ...
#include <glslang/Public/ResourceLimits.h>
// ...

std::vector<uint32_t> CompileGLSLToSPRIV(const std::string &source) {
    // ...

    shader.parse(
        GetDefaultResources(),  // default TBuiltInResource from ResourceLimits.h
        100,                    // default version
        false,                  // not forward compatible
        EShMsgDefault           // report default error/warning messages
    );
    // There're overloads for extra options like includers but we'll skip that for now

    printf("Parsing shader: %s\n", shader.getInfoLog()); // get the log for parsing the shader

    // ...
}
```

After that, we can simply create a `glslang::TProgram` object and link the shader:

```c++
std::vector<uint32_t> CompileGLSLToSPRIV(const std::string &source) {
    // ...

    glslang::TProgram program;
    program.addShader(&shader);
    program.link(EShMsgDefault);    // link and report default error/warning messages

    printf("Linking program: %s\n", program.getInfoLog()); // get the log for linking the program

    // ...
}
```

### Export SPIR-V bytes

If everything goes smoothly, we can now export the generated SPIR-V bytes.

First we need to include the utility function:

```c++
#include <glslang/SPIRV/GlslangToSpv.h>
```

It's pretty straight forward to get the result:

```c++
std::vector<uint32_t> CompileGLSLToSPRIV(const std::string &source) {
    // ...

    // get the vertex stage glslang intermediate representation from the program
    glslang::TIntermediate *intermediate = program.getIntermediate(EShVertex);

    std::vector<uint32_t> spriv;                    // the vector for the output
    glslang::GlslangToSpv(*intermediate, spirv);    // convert the glslang intermediate into SPIR-V bytes

    return spirv; // Usually the result is optimized with RVO so don't worry about copying
}
```

You can now pass the SPIR-V bytes to `VkShaderModuleCreateInfo` (or probably `glShaderBinary`? I don't know if anyone is actually using this 🙂).

---
title:  "SIMD Experiments"
excerpt: "Some experiments with SIMD instrinsics. The goal is to write a new SIMD math library for Haru-V engine."
header:
  teaser: /assets/images/simd/cover.png
  overlay_image: /assets/images/simd/cover.png
  overlay_filter: 0.5
  caption: "Screenshot of benchmarking"
  actions:
    - label: "GitHub"
      url: https://github.com/andyroiiid/SimdExperiments/
sidebar:
    - title: "Type"
      text: "Math Library"
    - title: "Programming Lanauges"
      text: "C++"
    - title: "Highlighted Features"
      text: "SIMD Intrinsics, Vector/Matrix/Quaternion Support"
    - title: "Team"
      text: "Solo"
    - title: "Work Period"
      text: "03/14/2022 - Present"
    - title: "GitHub Repository"
      text: "https://github.com/andyroiiid/SimdExperiments/"

toc: true
---

There was [a great talk on quaternions at GDC 2023 by Hamish Todd](https://schedule.gdconf.com/session/math-in-game-development-summit-a-visual-guide-to-quaternions-and-dual-quaternions/894472). I stayed in Room 2001 all day with [Prof. Squirrel](http://www.eiserloh.net/bio/) and those talks were amazing. You should definitely check the GDC Vault if you missed them!
{: .notice--success}

This project is still in early stage so there's not much to share, but here are some benchmarks I did.

The benchmarks are done on a Terrans Force AMD 27X7SH1 laptop. Here's the environment:
- CPU: AMD Ryzen 7 3700X 8-Core Processor 3.59 GHz
- RAM: 16GB DDR4 3200MHz
- Windows Version: Windows 10 Pro Version	22H2 OS build	19045.2728

Compiler flags impact these benchmark results **A LOT**, and if you force your structs to use 16 bytes alignment (`alignas(16)`), compiler might do **a much better job** at vectorization than your handwritten SIMD instructions.

A big lesson I learnt from this is to **do as many as benchmarks as you can with different compiler flags**.
{: .notice--warning}

## Vectors

### Normalization

| Name | Average Time |
| --- | --- |
| Plain Normalize | 5.1861 ns |
| SIMD Normalize (`_mm_sqrt_ps` + `_mm_div_ps`) | 2.26811 ns |
| **SIMD Fast Normalize (`_mm_rsqrt_ps` + `_mm_mul_ps`)** | 1.19543 ns |

### Cross Product

| Name | Average Time |
| --- | --- |
| Plain Cross Product | 4.63804 ns |
| **SIMD Cross Product** | 0.840373 ns |

## Matrices

### Matrix Multiplication

| Name | Average Time |
| --- | --- |
| Plain Matrix Multiplication | 19.6323 ns |
| **SIMD Matrix Multiplication** | 4.29214 ns |

### LookAt Matrix

| Name | Average Time |
| --- | --- |
| glm::lookAt | 28.2944 ns |
| **SIMD LookAt Matrix** | 1.91781 ns |

### Perspective Matrix

This one is kind of funny because I didn't really do anything SIMD other than using an aligned struct. There might be something wrong with `glm`'s implementation. It could also be me using `glm::perspective` in a wrong way?

| Name | Average Time |
| --- | --- |
| glm::perspective | 16.4587 ns |
| **SIMD Perspective Matrix** | 1.90413 ns |

## Quaternions

Quaternions are very funny. At first I tought I was doing a fantastic job optimizing with SIMD intrinsics. Then I added `alignas(16)` to those plain quaternion structs, and suddenly the compiler vectorized versions were blazing fast 😥.

My guess is that I was doing too much `_mm_shuffle_ps`. Might need to do some profiling with [AMD uProf](https://www.amd.com/en/developer/uprof.html) later.

### Hamilton Product

| Name | Average Time |
| --- | --- |
| **Plain Hamilton Product** | 0.240584 ns |
| SIMD Hamilton Product | 1.27795 ns |

### Matrix Conversion

| Name | Average Time |
| --- | --- |
| **Plain Matrix Conversion** | 1.91547 ns |
| SIMD Matrix Conversion | 1.95097 ns |

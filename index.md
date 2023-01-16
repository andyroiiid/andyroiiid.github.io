---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: splash

header:
  overlay_color: "#000"
  overlay_filter: "0.7"
  overlay_image: /assets/images/haru-v/screenshot.png
  actions:
    - label: "About Me"
      url: "/about"
    - label: "Portfolio"
      url: "/portfolio"
    - label: "Resume"
      url: "/resume"
  caption: "Screenshot of my personal game engine project: Haru-V"

title: "Andrew Huang"
excerpt: "Hi, I'm **An \"Andrew\" Huang**, a **Game Graphics/Engine Programmer**."

shipped_row:
  - image_path: /assets/images/covers/brain-machine.png
    title: "Brain Machine"
    excerpt: "A 3D puzzle/action game focusing on **polymorphing maps**. Shipped on **Steam**, **App Store**, and Chinese **Android** stores."
    url: "/portfolio/brain-machine"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/covers/hex-rally-racers.png
    title: "Hex Rally Racers"
    excerpt: "A split-screen multiplayer **racing** game. Shipped on **Steam**."
    url: "/portfolio/hex-rally-racers"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Conjury Revell"
    excerpt: "A **steampunk** first person shooter. **About to ship on Steam**."
    url: "/portfolio/conjury-revell"
    btn_label: "Read More"
    btn_class: "btn--primary"

haru_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Haru-V"
    excerpt: "A **Vulkan** 3D game engine with **Physically Based Rendering**, **Forward + Deferred Pipelines** and **Lua Scripting** support. It also integrates **FMOD** and **PhysX**. Somewhat inspired by **Quake/Source/early IW** Engines."
    url: "/portfolio/haru-v"
    btn_label: "Read More"
    btn_class: "btn--success"

personal_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Trenchbroom-Haru"
    excerpt: "A fork of the TrenchBroom editor, designed to use with **Haru-V engine** and serve as its **level editor**."
    url: "/portfolio/trenchbroom-haru"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Haru"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/covers/harujion.png
    title: "Harujion"
    excerpt: "A 2D **Modern OpenGL**-based game engine with **Lua** scripting support. Heavily inspired by **Love2D**."
    url: "/portfolio/harujion"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/covers/overtime.png
    title: "Overtime"
    excerpt: "A **Half-Life 2: Episode 2** map focusing on **Time Travel** abilities and gameplay. Heavily inspired by \"Effect and Cause\" from *Titanfall 2*."
    url: "/portfolio/overtime"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/covers/aseprite-importer.png
    title: "Aseprite Importer"
    excerpt: "***.aseprite** file (a pixel art format) importer for **Unity3D**."
    url: "/portfolio/aseprite-importer"
    btn_label: "Read More"
    btn_class: "btn--primary"

team_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Rolling Blocks"
    excerpt: "A **3D** mobile **block rolling** puzzle game. This is a cut project of **Brainagi Games**."
    url: "/portfolio/rolling-blocks"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/covers/nyanzo.png
    title: "Nyanzo: No Lives Left"
    excerpt: "A **2D** mobile **swipng puzzle** game."
    url: "/portfolio/nyanzo"
    btn_label: "Read More"
    btn_class: "btn--primary"

early_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Blockcraft"
    excerpt: "A **multi-threaded** Minecraft-like **voxel** game engine with **infinite world** support. It's one of my early projects."
    url: "/portfolio/blockcraft"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Free Fall"
    excerpt: "A **platforming puzzle** game made with **Blockcraft** engine. It's one of my early projects."
    url: "/portfolio/free-fall"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/covers/trace-r.png
    title: "TraceR"
    excerpt: "A toy **interactive** software **path tracer**. It's one of my early projects."
    url: "/portfolio/trace-r"
    btn_label: "Read More"
    btn_class: "btn--primary"
---

<h1><center>Shipped Games</center></h1>
<hr/>

{% include feature_row id="shipped_row" %}

<h1><center>Personal Projects</center></h1>
<hr/>

{% include feature_row id="haru_row" type="left" %}

{% include feature_row id="personal_row" %}

<h1><center>Team Projects</center></h1>
<hr/>

{% include feature_row id="team_row" %}

<h1><center>Early Projects</center></h1>
<hr/>

{% include feature_row id="early_row" %}

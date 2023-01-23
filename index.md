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
    - label: "Resume"
      url: "/resume"
  caption: "Screenshot of my personal game engine project: Haru-V"

title: "Andrew Huang"
excerpt: "Hi, I'm **An \"Andrew\" Huang**, a **Game Graphics/Engine Programmer**."

shipped_row:
  - image_path: /assets/images/brain-machine/cover.png
    title: "Brain Machine"
    excerpt: "A 3D puzzle/action game focusing on **polymorphing maps**. Shipped on **Steam**, **App Store**, and Chinese **Android** stores."
    url: "/shipped_games/brain-machine"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/temp.png
    title: "Hex Rally Racers"
    excerpt: "A split-screen multiplayer **racing** game. Shipped on **Steam**."
    url: "/shipped_games/hex-rally-racers"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/temp.png
    title: "Conjury Revell"
    excerpt: "A **steampunk** first person shooter. **About to ship on Steam**."
    url: "/shipped_games/conjury-revell"
    btn_label: "Read More"
    btn_class: "btn--primary"

haru_row:
  - image_path: /assets/images/haru-v/cover.png
    title: "Haru-V Engine"
    excerpt: "A **Vulkan** 3D game engine with **Physically Based Rendering**, **Forward + Deferred Pipelines**, **Casecade Shadow Map**, and **Lua Scripting** support. It also integrates **FMOD** and **PhysX**. Somewhat inspired by **Quake/Source/early IW** Engines."
    url: "/personal_projects/haru-v"
    btn_label: "Read More"
    btn_class: "btn--success"

personal_row:
  - image_path: /assets/images/temp.png
    title: "Strafe"
    excerpt: "A high-mobility first person shooter prototype with wall-running abilities."
    url: "/personal_projects/strafe"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/blockcraft/cover.png
    title: "Blockcraft Engine & Free Fall (Game)"
    excerpt: "A **multi-threaded** Minecraft-like **voxel** game engine with **infinite world** support, and a **plaforming** game made with the engine. It's one of my early projects."
    url: "/personal_projects/blockcraft"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/temp.png
    title: "More Personal Projects"
    excerpt: "I spent most of my free time working on my personal projects. Check the button for more."
    url: "/personal_projects"
    btn_label: "More Projects"
    btn_class: "btn--primary"
---

<h1><center>Shipped Games</center></h1>
<hr/>

{% include feature_row id="shipped_row" %}

<h1><center>Personal Projects</center></h1>
<hr/>

{% include feature_row id="haru_row" type="left" %}

{% include feature_row id="personal_row" %}

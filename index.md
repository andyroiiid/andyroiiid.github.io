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
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Brain Machine"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Hex Rally Racers"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Conjury Revell"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"

haru_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Haru-V"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--success"

personal_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Trenchbroom-Haru"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Haru"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Harujion"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Overtime"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Aseprite Importer"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"

team_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Nyanzo: No Lives Left"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"

early_row:
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Blockcraft"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "Free Fall"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--primary"
  - image_path: /assets/images/haru-v/screenshot.png
    title: "TraceR"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
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

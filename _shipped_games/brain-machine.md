---
title:  "Brain Machine"
excerpt: "A 3D puzzle game focusing on polymorphing maps and stealth. Shipped on Steam, App Store, and Chinese Android stores."
header:
  teaser: /assets/images/brain-machine/cover.png
  overlay_image: /assets/images/brain-machine/old_screenshot.jpg
  overlay_filter: 0.5
  caption: "Screenshot of Brain Machine (Steam version)"
  actions:
    - label: "Steam"
      url: https://store.steampowered.com/app/601120/Brain_Machine/
    - label: "TapTap (Server closed)"
      url: https://www.taptap.cn/app/67060
    - label: "App Store (Server closed)"
      url: https://apptopia.com/ios/app/1208346401/about
sidebar:
    - title: "Role"
      text: "Unity3D/Server Programmer & Technical Artist"
    - title: "Game Engine"
      text: "Unity3D 5"
    - title: "Genre"
      text: "3D, Puzzle, Sci-fi, Stealth"
    - title: "Team"
      text: "Brainagi Games, ~7 developers"
    - title: "Work Period"
      text: "07/2017 - 03/2019"
    - title: "Shipped Platforms"
      text: "Steam, iOS, Android"

gallery:
  - url: /assets/images/brain-machine/iphonex.jpg
    image_path: /assets/images/brain-machine/iphonex.jpg
    title: "Testing Brain Machine on iPhone X"
  - url: /assets/images/brain-machine/old_screenshot.jpg
    image_path: /assets/images/brain-machine/old_screenshot.jpg
    title: "Brain Machine Steam version"
  - url: /assets/images/brain-machine/new_screenshot.jpg
    image_path: /assets/images/brain-machine/new_screenshot.jpg
    title: "Brain Machine mobile version"
  - url: /assets/images/brain-machine/screenshot1.jpg
    image_path: /assets/images/brain-machine/screenshot1.jpg
    title: "More screenshots of Brain Machine"
  - url: /assets/images/brain-machine/screenshot2.jpg
    image_path: /assets/images/brain-machine/screenshot2.jpg
    title: "More screenshots of Brain Machine"
  - url: /assets/images/brain-machine/screenshot3.jpg
    image_path: /assets/images/brain-machine/screenshot3.jpg
    title: "More screenshots of Brain Machine"
  - url: /assets/images/brain-machine/screenshot4.jpg
    image_path: /assets/images/brain-machine/screenshot4.jpg
    title: "More screenshots of Brain Machine"
  - url: /assets/images/brain-machine/appstore.jpg
    image_path: /assets/images/brain-machine/appstore.jpg
    title: "Brain Machine on App Store"
---

## Gameplay Trailer (Steam version)

{% include video id="Cy47yWCmB3I" provider="youtube" %}

## Game Description

This is a 3D puzzle/action game focusing on polymorphing maps. Shipped on [Steam](https://store.steampowered.com/app/601120/Brain_Machine/), [App Store](https://apptopia.com/ios/app/1208346401/about), and [Chinese Android stores](https://www.taptap.cn/app/67060).

## My Responsibilities

This is my **first** project as a game programmer. We were a small team, so I had to **grow quickly** and pick up **all kinds of responsiblities**.

Here's a flowchart of the most roles I took:

```mermaid
graph TD

  Optimize[Optimize] --> Support[Graphics Support]
  Optimize --> Steam[Steam Release]
  Optimize --> Xbox[Xbox Experiments]
  Support --> Graphics[Graphics Overhaul]
  Steam --> Graphics
  Steam --> Mobile[Mobile Port]
  Graphics --> Mobile
  Mobile --> Refactor[Gameplay Refactor]
  Mobile --> iOS[iOS Port]
  Mobile --> Android[Android Port]
  Android --> Server[Game & In-App Purchase Server]

  subgraph Graphics Programmer
    Support
    Graphics
  end

  subgraph Gameplay Programmer
    Mobile
    Refactor
    iOS
    Android
  end

  subgraph Server Programmer
    Server
  end
```

At the beginning I didn't know much about the game, but I got some experience with Unity and OpenGL (and shaders). My first task was **maintaining the PC build**. Unity has a very mature pipeline, so my major resposibility was simply to watch and make sure nothing goes wrong. I also got the chance to study every parts of the game.

Later as I became a better game programmer and knew more about the project, I began working as a **Graphics Programmer** and helped the artists making new animations, models, and materials. I **wrote shaders with ShaderLab** and **made some VFX**.

After the game released on Steam, we continued to prepare for an iOS release. I was one of the only two developers with a Mac™ device so naturally I became a **Gameplay Programmer** when we found that we need to add a whole new system for touch screen support.

Yes, we were a small team so we had to BYOD.
{: .notice--success}
Yes, I was using a MacBook Pro with a mid-tier AMD GPU back then, which wasn't a great choice for making games.
{: .notice--success}
Yes, technically the game also runs on macOS. I believe I also made a build for Linux, but we never had plans to release on those platforms.
{: .notice--success}

The last platform we released on was Android, which became a whole new story, I'll talk about that [here](/anecdote/anecdote-releasing-an-android-game-in-china).

Anyway, we had to develop a game server to handle things like **purchasing and game cloud saves**. Again, as the only devloper with some knowledge on web services, I became a **Server Programmer**, **wrote our game server with Flask**, and **integrated with all kinds of purchasing services**.

## Gallery

{% include gallery %}

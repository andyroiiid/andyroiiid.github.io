---
title:  "Conjury Revell"
excerpt: "A steampunk first person shooter. Shiped on Steam. I worked on this project as a technical designer."
header:
  teaser: /assets/images/conjury-revell/cover.jpg
  overlay_image: /assets/images/conjury-revell/cover.jpg
  overlay_filter: 0.5
  actions:
    - label: "Steam"
      url: https://store.steampowered.com/app/2142850/Conjury_Revell/
sidebar:
    - title: "Role"
      text: "Technical Designer"
    - title: "Game Engine"
      text: "Unreal 4.27.2"
    - title: "Genre"
      text: "3D, Spell, First-Person Shooter"
    - title: "Team"
      text: "SMU Guildhall, ~30 developers"
    - title: "Work Period"
      text: "06/2022 - 12/2022"
    - title: "Shipped Platforms"
      text: "Steam (planning)"
toc: true
---

## Game Trailer

{% include video id="cdayA9Rxa9w" provider="youtube" %}

## My Responsibilities

### Preprodution

- Brainstormed for game ideas.
- Programmed several game prototypes in Unreal 4 engine.
- Explored Houdini pipeline. Grabbed an small part of London from the map and made a procedural area with it.

### Production

- Explored [Gameplay Ability System](https://docs.unrealengine.com/5.1/en-US/gameplay-ability-system-for-unreal-engine/) and made some experiments.
- Brainstormed for spell ideas.
- Made action blocks for monorail cars, ziplines, and other systems.
- Designed some candidate levels.
- Programmed basically every spline-based object in the game.
  - Ziplines
  - Procedural pipes and modular kits
  - Conveyor Belts
  - Monorail cars
- Provided programming and technical art support for the VFX team.
- Helped the animation team on character animations.
- Helped the sound team, implemented several sound effects, and made the system for ambient sound.
- Fixed aesthetics and performance issues on lighting together with the lead artist.

## Houdini Preproduction

During the preproduction stage, I was the sole developer responsible for exploring integrating Houdini into our pipeline.

I teamed up with another level designer and made a sample level of using Houdini to procedurally generate a city background.

{% include video id="f7p_rbfr6Aw" provider="youtube" %}

I also made some other experiments like using Houdini to procedurally generate pipline systems or create damaged assets.

In case you don't know, a Houdini evangelist from SideFX comes to our school every year. He just visited us again yesterday as of this writing, and somehow we couldn't even use Houdini in our capstone projects 🙂. Thanks to SideFX's confusing licensing policy, we had to give up Houdini eventually.
{: .notice--info}

## Zipline System

I made the zipline system for the game. The code for this was actually based on the zipline system from my personal project [Strafe](/personal_projects/strafe/). I was the sole programmer for this feature.

### POCT (Proof of Concept: Technology)

The prototype zipline uses an actual rope and moves the player between two points.

It's pretty simple but looks believable without any animation.

{% include video id="Cg6lzBcnFm0" provider="youtube" %}

### Zipline Action Block

Later we decided that the zipline should look like some sort of magical power line, so the zipline no longer uses an actual rope.

I wrote some code to procedurally generate meshes for ziplines. There were two versions of ziplines:

- Direct (a straight line)
- Spline-based (basically any shape a spline can make)

At this point the zipline is basically usable so I started putting up some action blocks with ziplines.

Here's one action block I made. It's heavily inspired by the "Shantytown Police Station" in *BioShock Infinite*.

{% include video id="5fjDhNN4x-I" provider="youtube" %}

### The zipline version that was put into production

I kept working on the ziplines for a while and in the final version the player can easily jump onto and off any zipline at anytime.

This gives the player great movement flexibility and it feels nice riding the ziplines.

Here's a simple zipline challenge action block I made (the player has double jump ability):

{% include video id="Uj7plq8Vejo" provider="youtube" %}

Unfortunately, the zipline system eventually got cut along with tons of other features and levels.
{: .notice--danger}

## Monorail System

I brought up the original idea of this gameplay element. Basically it can work as a way of transportation and also a tool to spawn enemies at any location. It has several nice features:

- It's **flexible** but **predictable**: we can move a monorail to any location along the rail and players can easily anticipate the movement.
- **Audio** and **visual** hint: Imagine a monorail moving in with sirens on and flashing lights. It's impossible for the player to miss it.
- **Cool** and **fits the theme**: Our game has a steampunk theme, and it plays well with monorail cars.

I still have a video of the early monorial prototype. As you can probably guess, I scrapped a prototype train model, turned it upside down, and pretended it's a monorail car. Monorail cars will try to find a location on the rail closest to the player and drop enemies.

I was showcasing that monorail cars can be spawned from both directions, so please ignore those two cars that clipped through each other.🙂
{: .notice--info}

{% include video id="tBFESnHx87s" provider="youtube" %}

However, Monorail ended up being another system that died very early because we didn't have enough artists to work on the animation.
{: .notice--danger}

## Wherever the team needs me

I got experience in a lot of areas thanks to [my indie studio experience](/shipped_games/brain-machine), so I was also put in all kinds of positions because those teams need my help:

- Helped the VFX team make some visual effects.
- Helped the animation team with character animations.
- Helped the sound team because the milestone was near and they still needed tons of sound effects.
- Helped basically whoever needs my help.

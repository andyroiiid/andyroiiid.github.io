---
title:  "Overtime"
excerpt: "A **Half-Life 2: Episode 2** map focusing on **Time Travel** abilities and gameplay. Heavily inspired by \"Effect and Cause\" from *Titanfall 2*."
header:
  teaser: /assets/images/overtime/cover.jpg
  overlay_image: /assets/images/overtime/cover.jpg
  overlay_filter: 0.5
  caption: "A composed screenshot of two timelines in Overtime"
sidebar:
    - title: "Type"
      text: "Custom Map"
    - title: "Game"
      text: "Half-Life 2: Episode 2"
    - title: "Highlights"
      text: "Time travel; A balanced mix of action, shooting, and puzzles"
    - title: "Team"
      text: "Solo"
    - title: "Time Spent"
      text: "~50 hours"
gallery:
  - url: /assets/images/overtime/cover.jpg
    image_path: /assets/images/overtime/cover.jpg
    title: "Timeline switching"
  - url: /assets/images/overtime/screenshot1.jpg
    image_path: /assets/images/overtime/screenshot1.jpg
    title: "Present"
  - url: /assets/images/overtime/screenshot2.jpg
    image_path: /assets/images/overtime/screenshot2.jpg
    title: "Future"
  - url: /assets/images/overtime/screenshot3.jpg
    image_path: /assets/images/overtime/screenshot3.jpg
    title: "First combat area"
  - url: /assets/images/overtime/screenshot4.jpg
    image_path: /assets/images/overtime/screenshot4.jpg
    title: "Time travel puzzle"
  - url: /assets/images/overtime/screenshot5.jpg
    image_path: /assets/images/overtime/screenshot5.jpg
    title: "Heavy combat"
  - url: /assets/images/overtime/screenshot6.jpg
    image_path: /assets/images/overtime/screenshot6.jpg
    title: "Time travel action puzzle"
  - url: /assets/images/overtime/screenshot7.jpg
    image_path: /assets/images/overtime/screenshot7.jpg
    title: "Vent (just like Titanfall 2)"
  - url: /assets/images/overtime/screenshot8.jpg
    image_path: /assets/images/overtime/screenshot8.jpg
    title: "Final boss"
---

This level is implemented using only vanilla Half-Life 2 entities (without any C++ mod or VScript).
{: .notice--success}

## Gameplay Trailer

{% include video id="Hx9MBTa_L8I" provider="youtube" %}

## Design Trailer

{% include video id="kU3r6afn8w8" provider="youtube" %}

## Gallery

{% include gallery %}

## Inspiration

This level is inspired by “Effect and Cause” from Titanfall 2 and “A Crack in the Slab” from Dishonored 2 where players can switch between two versions of the same place.

## Scripting: How to implement time-travel with only Half Life 2 entities?

### Prelude: implementing Portal in Half Life 2

Last year, I tried to implement the Portal mechanic in Half Life 2 using only Half Life 2 entities.

After some simple experiments, I discovered that I can use `func_monitor` and `trigger_teleport` to make portals.

The solution is not perfect, because the correct way to implement portals is rendering the scene with another camera (or several cameras) and use stencil testing to discard unused pixels.

Unfortunately, I encountered two problems:

1. The Half Life 2 version of Source Engine only allows ONE active `point_camera` at any time, which makes it impossible to show two portals at the same time.

2.  Players will lose velocity when teleported using `trigger_teleport`, and they can't carry objects with them through portals.

These limitations made it pretty hard for me to make anything interesting. The level turned out to be very boring, but I still learned a lot about Half Life 2 and Source Engine.

### Movement, velocity and logic_measure_movement

{% include video id="IH1BSHTNI8I" provider="youtube" %}

I read tons of Half Life 2 and Source Engine documentations when trying to solve those problems with portals. Even though I didn't solve them, I gradually got a grasp on how to do all kinds of stuff in Half Life 2 and Hammer. Some entities will reset the players' velocity, and some won't. Some entities only work in multiplayer, and some entities won't work at all 😅.

Then, a special entity caught my attention when I was trying to design my second HL2 level: `logic_measure_movement`. Logic entities in Half Life 2 are very powerful (if you know how to use them). Basically, what `logic_measure_movement` does is to copy an object's movement to another object.

In Half Life 2 there's another entity called `point_teleport`. It's a widely used entity, but there's a big limitation with it: you cannot change the target location at runtime. But if you combine `logic_measure_movment` with `point_teleport` and guess what? Now you can change the target teleportation location! There's also a bonus with this: players don't lose velocity when teleporting!

![Hammer screenshot](/assets/images/overtime/hammer.png)

This is how I implemented the time-travel mechanic. I made two versions of the same world in two timelines, and used those entities to synchronize players' location and teleportation targets. You can see the video for the final effect. It's seamless.

## Design: Iteration of the Final Boss Fight

### Version 1: Find an angle and shoot

![Version 1](/assets/images/overtime/design/1.jpg){: .align-right}

In the original version of the boss fight, players need to discover the opening behind the glass cage, and shoot the antlion to kill it.

However, there are some issues with this design:

1. It's hard to see the opening.

2. Putting an antlion in an open cage and not letting it fly around is strange.

### Version 2: Platforming challenge

![Version 2](/assets/images/overtime/design/2.jpg){: .align-right}

To solve that issue, I sealed the cage and changed the gameplay to platform jumping (just like the action block demo).

It kind of solved the previous issue, but new issues appeared:

1. Platform jumping is too hard for some players.

2. Players have no interaction with the antlion guardian at all because they are on the platforms, and the antlion guardian cannot reach them.

### Version 3 (final): Physics interaction

![Version 3](/assets/images/overtime/design/3.jpg){: .align-right}

Eventually, I came up with this version: shooting explosive barrels to destroy the pillars, and time-shifting into the cage to kill the small antlion.

It's not a perfect solution, but I think it solved previous issues well enough, so I decided to stick with this version.

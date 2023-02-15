---
title:  "Strafe"
excerpt: "A high-mobility first person shooter prototype with **wall-running** abilities like *Titanfall 2*. My master's thesis is also related to this project."
header:
  teaser: /assets/images/strafe/cover.png
  overlay_image: /assets/images/strafe/movement.png
  overlay_filter: 0.5
sidebar:
    - title: "Type"
      text: "Game Prototype"
    - title: "Game Engine"
      text: "Unreal 4 / Source SDK 2013"
    - title: "Programming Lanauges"
      text: "C++, Unreal Blueprints"
    - title: "Highlighted Features"
      text: "Wall Running; Double Jumping; Mantling"
    - title: "Team"
      text: "Solo"
toc: true
---

This project is still a work-in-progress.
{: .notice--danger}

## Kaiju Killer: The game that was never made

During the preproduction stage of [Conjury Revell](/team_games/conjury-revell), I brought up a quite ambitious project idea and we made a Flash Hack prototype for it. The core idea was that players are superhuman soldiers that can **run on walls** and fight Kaijus with all kinds of weapons.

It looks very cool and probably too cool to be true so that we decided that we were not worthy of making it.

That was just joking. We didn't pick this idea because it was way too overscoped and we only had one animation artist. 🙂
{: .notice--info}

{% include video id="CF5McWboXwY" provider="youtube" %}

## Strafe: Reborn

I wrote the code for wall running and other movement mechanics in Kaiju Killer. After the idea was abandoned, I thought that it was too wasteful to throw the code away, so I cleaned up the code and rewrote it from **Blueprint** into **C++**. The new project is now named *Strafe*.

### Strafe Movement Demo Video

After the rewrite, the movement code became much more robust and can now work properly on moving platforms.

{% include video id="LEeeKLWwMaE" provider="youtube" %}

### Fixing movement on moving platforms

There's a system called [Movement Base](https://docs.unrealengine.com/4.27/en-US/BlueprintAPI/Pawn/Components/CharacterMovement/GetMovementBase/) in Unreal. Basically it makes a pawn inherit the velocity of the platform it stands on.

However, there are two problems with this system:

1. Wall running doesn't count as "standing" on a platform.
2. The second jump in double jumps doesn't have a valid movement base, and thus might produce unexpected bugs.

For the **first** problem, it's easy: just manually update the movement base when wall running.

For the **second** problem, it becomes complicated. Sophisticated games like Titanfall 2 still have some weird bugs caused by this problem: (I didn't make this video)

{% include video id="2uiL9Dgxwms" provider="youtube" %}

Yes, I'm a fan of Titanfall.
{: .notice--success}

Basically, when the player leaves a moving platform, we have three options.

1. Lose the movement base and thus inherit no velocity from it.
2. Keep the movement base **reference** and move with it.
3. Keep the movement base **velocity**.

![Jump Probglem](/assets/images/strafe/jump-problem.png){: .align-center}

Obviously, the **first** option, which is the *Unreal* default, is a bad one. Imagine going up on a fast elevator, you won't be able to double jump at all if the elevator's speed is faster than your jump speed.

*Titanfall* uses the **second** option. It works nicely most of the time, but if the platform is changing directions frequently and you are double jumping towards a static reference, you' ll see some weird stuff like the video above.

Therefore, I'm using a **thrid** option in *Strafe*:

> The player character inherits the velocity of the object it last touches.

This is actually a **physical** solution because character speed changes are generally caused by friction. That's why characters can stand on platforms and move with them.

Friction can only happend between touching objects, so whenever the player character touches the ground or walls, the player gets the velocity of that object. When players jump into the air, they can still keep that velocity (because of inertia).

The final result ([the movement demo video above](#strafe-movement-demo-video)) is good enough for me.

## Going Fast: My master's thesis

I'm currently working on my master's thesis:

> Going Fast: Map Design for High Mobility First Person Shooter

Basically it talks about the common practices and principles I discovered for this movement mechanics, but I cannot share more details on that yet.

Due to some school limitations I couldn't use my Strafe project for this thesis, so I was working on a Source SDK 2013 mod based on [Mobility Mod for Half-Life 2](https://www.moddb.com/mods/mobility-mod-for-half-life-2). The code was written for the original Source SDK, but I didn't want to use the super old Visual Studio 2013 tool chain, so I migrated the code to [source-sdk-2013-ce](https://github.com/Nbc66/source-sdk-2013-ce), which supports the newer Visual Studio versions.

### Wingman: Playtest Data Collection System

Even though I currently cannot share the details on my thesis yet, I can still share with you the playtest data collection system I made for my thesis.

The data collection system is called [Wingman](https://github.com/andyroiiid/wingman). I turned it into a Docker container and deployed to Google Cloud, so that my playtesters can play on their computers at any time without me standing there watching them playing.

I then wrote an in-game visualization system to visualize the collected data in Source Engine.

![Wingman In-game Visualization](/assets/images/strafe/wingman-vis.png)

The **lines** are the players' movement routes, and the **spheres** are actions like starting/ending wall running and double jumping.

I'll share more details when I finish my thesis.
{: .notice--info}


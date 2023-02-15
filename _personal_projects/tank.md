---
title:  "Tλnk"
excerpt: "A **Half-Life 2: Episode 2** map with a drivable tank."
header:
  teaser: /assets/images/tank/cover.jpg
  overlay_image: /assets/images/tank/cover.jpg
  overlay_filter: 0.5
  caption: "A screenshot of the whitebox/technical demo."
sidebar:
    - title: "Type"
      text: "Custom Map"
    - title: "Game"
      text: "Half-Life 2: Episode 2"
    - title: "Highlights"
      text: "Vehicle driving; Level scripting; Combat Design"
    - title: "Team"
      text: "Solo"
    - title: "Time Spent"
      text: "Work in Progress"
toc: true
---

This level is implemented using only vanilla Half-Life 2 entities (without any C++ mod or VScript).
{: .notice--success}

This level is still a work-in-progress.
{: .notice--danger}

## Technical/Whitebox Demo

{% include video id="YAdPY7PHCvE" provider="youtube" %}

## Tank Implementation

### Vehicle Physics

The tank itself is created using [`func_physbox`](https://developer.valvesoftware.com/wiki/Func_physbox) and [`phys_hinge`](https://developer.valvesoftware.com/wiki/Phys_hinge).

I believe it's also possible to add some suspension system using [`phys_spring`](https://developer.valvesoftware.com/wiki/Phys_spring), but that's not my top priority yet.

The "engine" is implemented using [`phys_thruster`](https://developer.valvesoftware.com/wiki/Phys_thruster) and [`phys_torque`](https://developer.valvesoftware.com/wiki/Phys_torque), so it's using single-point physics (like Mario Kart) instead of a realistic vehicle physics system.

### Tank gun

The tank gun is implemented using [`func_tankrocket`](https://developer.valvesoftware.com/wiki/Func_tankrocket). The player will automatically "use" the tank gun when they enter the driver seat.

### User Interface

The driver seat is a [`trigger_multiple`](https://developer.valvesoftware.com/wiki/Trigger_multiple). When the player enters the driver seat, it:

- Uses [`game_ui`](https://developer.valvesoftware.com/wiki/Game_ui) to freeze players and hijack their input.
- Sends out a command to [`point_clientcommand`](https://developer.valvesoftware.com/wiki/Point_clientcommand) to simulate crouch input (thus forcing the player to crouch)

## Fixing the steering direction issue

There's one issue worth mentioning here, which is the steering direction.

- **In real life**, if you steer left when reversing, the car will turn right.
- **In the implementation described above**, the car will turn left, which is wrong.

If this is Unity or Unreal, it's super easy to solve this problem. You just add a branch to check if the vehicle is reversing.

However in Hammer this becomes complicated, because:

- Everything is event driven. You simply can't check input every frame.
- It's painful to setup branching logic using [`logic_branch`](https://developer.valvesoftware.com/wiki/Logic_branch). You'll need to dispatch an extra "Test" event to get the result.

Luckily, there's another way to do this: we can easily connect/disconnect logic at runtime using [`logic_relay`](https://developer.valvesoftware.com/wiki/Logic_relay). Basically, `logic_relay` allows you to "relay" logic, and you can enable/disable `logic_relay` at runtime.

So instead of branching, I simply dispatch both "turn left" and "turn right" command to `logic_relay`s, and turn them on and off based on whether the tank is moving forward. If you think about it, it's actually kind of like [functional programming](https://en.wikipedia.org/wiki/Functional_programming).

### Event dispatching route when driving forward

![Forward](/assets/images/tank/forward.png)

### Event dispatching route when reversing

![Reverse](/assets/images/tank/reverse.png)

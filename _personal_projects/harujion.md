---
title:  "Harujion Engine"
excerpt: "A 2D **Modern OpenGL**-based game engine with **Lua** scripting support. Heavily inspired by **Love2D**."
header:
  teaser: /assets/images/harujion/flappy.png
  overlay_image: /assets/images/harujion/flappy.png
  overlay_filter: 0.5
  caption: "Screenshot of Flappy Bird made with this engine"
sidebar:
    - title: "Type"
      text: "2D Game Engine"
    - title: "Programming Lanauges"
      text: "C++, Lua"
    - title: "Highlighted Features"
      text: "OpenGL renderer; Lua scripting; FMOD integration"
    - title: "Team"
      text: "Solo"
    - title: "Work Period"
      text: "06/13/2021 - 06/25/2021"
    - title: "GitHub Repository"
      text: "https://github.com/andyroiiid/harujion"

toc: true
---

In case you don't know, back in 2021 travelers in China would sometimes get quarantined for possible contact with COVID carriers. During the quarantine we need to stay in a designated hotel or something for two weeks.
{: .notice--success}

Harujion is a small 2d engine I made during quarantine (because I got nothing else to do). It's heavily inspired by [Love2D](https://love2d.org/).

I'm working on a similar project with one of my friend called `amore2d`. It's not ready for release yet, but now that I'm much more familiar with Lua APIs, I made a much better Lua-C++ interop layer.

## Features

- Modern OpenGL 2D Renderer (4.5 Core Profile, Direct State Access)
- Uses LuaJIT instead of vanilla Lua
- Lua Scripting Support
  - Window
  - Keyboard
  - Mouse
  - Renderer
  - Audio
  - Built-in common 2D graphics objects

## Demo video: Flappy Bird

{% include video id="n5nEM4SKz-g" provider="youtube" %}

Assets are from [this](https://github.com/sourabhv/FlapPyBird) repo.
{: .notice--info}

## Sample Lua Code: Player script for the Flappy Bird game

This is a simple piece of code I used in the Flappy Bird game. It's mainly for demo purpose so there's nothing fancy in it, but it works well.

```lua
-- load classic.lua for Lua OOP
local Object = require("classic.lua")

-- declare the Player class
local Player = Object:extend()

-- Player constructor
function Player:new()
    -- load the animation sprites
    self.sprites = {
        haru.Sprite.new("flappy/yellowbird-midflap.png", 32),
        haru.Sprite.new("flappy/yellowbird-downflap.png", 32),
        haru.Sprite.new("flappy/yellowbird-midflap.png", 32),
        haru.Sprite.new("flappy/yellowbird-upflap.png", 32)
    }
    self.v = 0.0 -- vertical velocity
    self.y = 0.0 -- vertical position
    self.sprite_timer = 0.0 -- animation timer
    self.sprite_idx = 1 -- current animation frame
end

function Player:jump()
    -- jumping is simply changing the vertical velocity
    self.v = 5.0
end

function Player:update(deltaTime)
    -- update velocity and position
    self.v = self.v - 10 * deltaTime
    self.y = self.y + self.v * deltaTime

    -- update sprite frame animation
    self.sprite_timer = self.sprite_timer + deltaTime
    if self.sprite_timer > 0.1 then -- 0.1s per animation frame
        self.sprite_timer = self.sprite_timer - 0.1

        self.sprite_idx = self.sprite_idx + 1 -- show next frame
        if self.sprite_idx == 5 then -- wrap back to the first frame
            self.sprite_idx = 1
        end
    end
end

function Player:draw()
    -- draw the sprite and rotate it based on velocity
    self.sprites[self.sprite_idx]:draw(0.0, self.y, self.v * 0.1)
end

return Player
```

## Lua APIs

I loosely followed the Love2D API (which is basically a wrapper around [SDL](https://www.libsdl.org/) and [SDL_Renderer](https://wiki.libsdl.org/SDL2/SDL_Renderer)).

### Window

- `haru.window.close()`: Close the window
- `haru.window.getFramebufferSize()`: Get the framebuffer size
- `haru.window.setTitle(title)`: Change the window title

### Keyboard

- `haru.keyboard.pressed(key)`: Check if a key is being pressed
- `haru.keyboard.justPressed(key)`: Check if a key is pressed in this frame
- `haru.keyboard.justReleased(key)`: Check if a key is released in this frame

### Mouse

- `haru.mouse.pressed(button)`: Check if a mouse button is being pressed
- `haru.mouse.justPressed(button)`: Check if a mouse button is pressed in this frame
- `haru.mouse.justReleased(button)`: Check if a mouse button is released in this frame
- `haru.mouse.normalizedPosition()`: Get mouse normalized position (0.0 ~ 1.0)
- `haru.mouse.setCursor(enable)`: Enable or hide the cursor

### Renderer

- `haru.renderer.setMatrixOrtho(left, right, bottom, top)`: Set the camera matrix
- `haru.renderer.setClearColor(r, g, b[, a])`: Change the renderer clear color
- `haru.renderer.setDrawColor(r, g, b[, a])`: Change the renderer draw color
- `haru.renderer.drawPoint(x, y[, size])`: Draw a point
- `haru.renderer.drawLine(x0, y0, x1, y1[, width])`: Draw a line
- `haru.renderer.drawRect(x0, y0, x1, y1[, width])`: Draw a rect (only the outline)
- `haru.renderer.fillRect(x0, y0, x1, y1)`: Fill a rect with draw color

### Audio

- `haru.audio.loadBank(filename)`: Load a FMOD audio bank
- `haru.audio.setVolume(volume)`: Change the global volume
- `haru.audio.getEventDescription(eventPath)`: Get the event description for a FMOD event
- `haru.audio.fireOneShotEvent(event)`: Play a one-shot FMOD event

### Built-in Lua Objects (Texture, Sprite, SpriteFont, Tileset)

**Texture**

- `haru.Texture.load(filename, filter, clamp, mipmap)`: Load a texture (returns a texture object)
- `haru.Texture:getSize()`: Get the texture size

**Sprite**

- `haru.Sprite.new(texture)`: Create a sprite from a texture
- `haru.Sprite:setPixelRect(x, y, w, h)`: Set the sprite to use a rect on a texture atlas (in pixels)
- `haru.Sprite:setPixelPivot(x, y)`: Set the sprite pivot (in pixels)
- `haru.Sprite:setFlip(x, y)`: Set the sprite to flip horizontally or vertically
- `haru.Sprite:draw(x, y, rotation, scaleX, scaleY)`: Draw the sprite

**SpriteFont**

- `haru.SpriteFont.new(fontFilename)`: Load a sprite font (bitmap font)
- `haru.SpriteFont:getGlyphPixelSize()`: Get the size of one glyph in the bitmap font
- `haru.SpriteFont:draw(x, y, text, size)`: Draw text using the sprite font

**Tileset**

- `haru.Tileset.new(texture, tileWidth, tileHeight, spacing)`: Load a tileset
- `haru.Tileset:getTileSize()`: Get the size of one tile in the tileset
- `haru.Tileset:draw(index, x, y)`: Draw the `index`th tile in the tileset

# SkyHop

A timed 2D platformer written in Java. Clouds fall from the sky, and you have 30 seconds to hop across as many of them as you can. You score a point the first time you land on each cloud.

![SkyHop gameplay](screenshot.png)

## How to play

| Key | Action |
|-----|--------|
| `A` / `D` | Move left / right |
| `W` | Jump (fly upward) |
| `S` | Drop down faster |

Click **PLAY** on the start screen. When the 30 seconds are up, the end screen shows your score and lets you play again.

## How it works

- **Game loop.** `Window` runs a fixed-timestep loop on its own thread. Game logic updates 60 times a second no matter how fast the machine renders, so the game plays at the same speed everywhere.
- **Rendering.** Each frame is drawn to a back buffer with a `BufferStrategy` and then shown all at once (double buffering), which prevents flicker.
- **Physics.** `Player` applies gravity every tick by increasing vertical velocity up to a terminal speed. Jumping sets an upward velocity.
- **Collision detection.** The player and each cloud have a bounding rectangle. When the player is falling and overlaps a cloud, they snap onto its top and stop falling. The first landing on a cloud scores a point and changes the cloud's image.
- **Cloud recycling.** Clouds drift down each tick. When one leaves the bottom of the screen, it's removed and a new one spawns at a random position, so there are always 8 clouds on screen.
- **Screens.** `StartPage` and `EndPage` are Swing windows. A Swing `Timer` ends the round after 30 seconds.

## Project structure

| File | What it does |
|------|--------------|
| `Main.java` | Entry point; opens the start screen |
| `StartPage.java` | Start screen with instructions and a Play button |
| `Window.java` | Game window, game loop, rendering and cloud spawning |
| `Player.java` | Player movement, gravity, collisions and scoring |
| `Cloud.java` | A single cloud: position, image and bounding box |
| `CloudGenerator.java` | Bounds for random cloud placement |
| `KeyboardHandler.java` | Maps W/A/S/D key presses to player movement |
| `EndPage.java` | Game-over screen with the final score |

## Run it

Requires Java 17 or later.

```bash
mkdir -p out/CloudGame
javac -d out *.java
cp *.png out/CloudGame/
java -cp out CloudGame.Main
```

## Built with

Java, Swing and AWT. No external libraries.

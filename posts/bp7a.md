---
title: Web Audio API & Responding to Text.
published_at: 2025-04-17
snippet: Week 7a
disable_html_sanitization: true
allow_math: true
---

# AT2 Accompaniment – Programming Concepts Used

This project is an interactive, generative 3D art piece that responds to user input by spawning jiggling jelly-like cubes connected in a chaotic, colorful web, with an earthquake sound to evoke the hidden energy of fungal life. Inspired by the article What Is It Like to Be A Fungus?, I wanted to express the idea that fungi are everywhere, pulsing beneath the surface, sometimes causing visible shifts in the world—like an earthquake.

Below, I describe how I used different programming concepts in this work.

# Variables

Variables are used to store the state of the program and reusable data:

` let t = 0;` — used to drive animation timing and background changes.

`let jellyTrail = [];` — stores all the jellies that are spawned.

`let rumbleSound;` — holds the loaded earthquake sound.

`let isActive = false;` — a boolean flag to track whether the sound and spawning are active.

# Iteration

Iteration is used to loop through arrays and update or draw multiple jelly cubes and connections:

```js
for (let i = 0; i < jellyTrail.length; i++) { ... }
```

In `draw()`, this loop animates each jelly object.
In `drawRainbowWeb()`, nested loops draw lines between pairs of jellies:

```js
 for (let i = 0; i < jellyTrail.length; i++) {
  for (let j = i + 1; j < jellyTrail.length; j++) {
    ...
  }
}
```

This creates a web of colored lines based on distance.

# Functions

Functions organize the code and perform specific tasks:

`preload()` loads the sound file.

`setup()` initializes the canvas and audio.

`draw()` runs every frame to render visuals.

`mousePressed()` toggles activity and starts sound/spawning.

`spawnJellyRecursively()` adds new jelly objects with recursion.

`drawRainbowWeb()` connects nearby jellies with colorful lines.

# Boolean Logic

Boolean logic is used to control whether things happen or not:

```js
if (isActive) {
  rumbleSound.play();
  spawnJellyRecursively(0);
} else {
  rumbleSound.stop();
}
```

Also:

```js
if (count >= 200 || !isActive) return;
```

This line ensures recursive spawning stops when the limit is reached or when the system is toggled off.

# Arrays

Arrays are used to store and manage all the jelly cubes:

```js
let jellyTrail = [];</pre>
```

Each jelly is an object with properties like `x, y, z,` and `time`, and is added using `jellyTrail.push(...)`.
This array is looped through in both the animation and the rainbow web drawing.

# Classes

My code does not define a custom class, but I used object literals like this:

```js
jellyTrail.push({ x: x, y: y, z: z, time: t, life: 0 });</pre>
```

This is similar to using classes but in a simplified way.

# Recursion

I used recursion to create a continuous jelly-spawning effect:

```js
function spawnJellyRecursively(count) {
  if (count >= 200 || !isActive) return;

  // Spawn a jelly...

  setTimeout(() => {
    spawnJellyRecursively(count + 1);
  }, 50);
}
```

This function calls itself with a delay, giving the feeling of an organic, growing system which is very appropriate for modeling fungal behavior.

# Artistic Choice: Earthquake Sound

I chose the sound of an earthquake because it complements the visual theme of jiggling jelly. Rather than using a literal or calm sound, I leaned into chaos as a creative principle. Inspired by What Is It Like to Be A Fungus?, I imagined fungi as not just passive decomposers but as powerful, disruptive forces hidden under the surface—like earthquakes.

The jellies jiggle as if reacting to an unseen tremor. The earthquake sound makes the invisible tension audible. It reminds us that fungi and mycelium networks can be subtle or destructive, shaping ecosystems in unpredictable ways. The chaotic aesthetic aligns with this theme.

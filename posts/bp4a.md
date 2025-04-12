---
title: Canvas API, Recursion, & Effective Complexity
published_at: 2025-03-25
snippet: Week 4a
disable_html_sanitization: true
allow_math: true
---

# Exploring Three Visual Compositions Using the p5.js Editor.

<iframe id="sketch" src="https://editor.p5js.org/Ranianazz/full/mDjByF8sv"></iframe>

<script type="module">

    const iframe  = document.getElementById ("sketch")
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width * 9 / 16 + 42

</script>

To create this high compressibility sketch, I followed a step-by-step tutorial from The Coding Train. It involved a lot of math; however, after following the tutorial, the math began to make sense. I was inspired by how beautiful the rainbow fern looked. I searched for ways to add colour to it and discovered the `colorMode(HSB, 360, 100, 100)` function, which I thought would transform it into a rainbow fern. Unfortunately, it didn't work as expected, so I conducted further research and found that I also needed to change the stroke settings. I used `stroke(hue, 80, 100);` and `strokeWeight(1.5);` along with `let hue = map(y, 0, 10, 120, 360);`. After adjusting the draw function, I finally achieved the desired look.

<iframe id="sketch2" src="https://editor.p5js.org/Ranianazz/full/gWsmrYMGs"></iframe>

<script type="module">

    const iframe  = document.getElementById ("sketch2")
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width * 9 / 16 + 42

</script>

I followed a step-by-step Coding Train tutorial to create this sketch. I consider it high effective complexity because it combines interactive growth (mousePressed) with structured branching and randomness in tree shapes and falling leaves.

<iframe id="sketch3" src="https://editor.p5js.org/Ranianazz/full/YgYiDt_yc"></iframe>

<script type="module">

    const iframe  = document.getElementById ("sketch3")
    iframe.width  = iframe.parentNode.scrollWidth
    iframe.height = iframe.width * 9 / 16 + 42

</script>

I utilised another step-by-step tutorial to create this low-compressible sketch. The sketch uses Perlin noise to smoothly move a circle across the screen. I’d say it has low compressibility because it utilises noise to create an output that is predictable and simple—there’s structure, but little surprise or complexity.

# Philip Galanter perspective on genereative art

In my opinion, Philip Galanter’s article suggests that generative art is any art created using a system that operates autonomously. His notion that “structure is subjective and remains in the eye of the beholder” indicates that generative art can be broad enough to encompass both past and future expressions. It can serve as a subset of all art, adapting as artistic practices evolve over time. This perspective is useful because it allows for a wide range of interpretations and evolving forms within generative art.

<div style="height: 100px;"></div>

---
title: Signals & three.js (cont.)
published_at: 2025-04-10
snippet: Week 6a
disable_html_sanitization: true
allow_math: true
---

# q5.js

q5.js is a beginner-friendly learning library that is compatible with p5.js. There are many clubs to join that serve as learning platforms, covering a wide range of genres from apps and software to comedy and illustration.

c2.js is similar to q5.js; however, it is primarily based on a JavaScript library for creative coding. It utilises geometric shapes, simulations, algorithms, and other modules to create digital interactive artworks.

SVG.js is a platform that uses code to create animated images. It offers a faster and more efficient method of coding, as it is easier to read and requires less code to animate an image.

Q5.js is a JavaScript learning platform that is compatible with p5.js. Q5.js could be used within a JavaScript library through ESM. Additionally, Svg.js can be utilised within a JavaScript module, as it is an XML-based vector format for graphics and images. This library can manipulate DOM and SVG elements effectively. On the other hand, c2.js is written in TypeScript and is released as a JavaScript library. It is primarily used for generating data visualisations, sound visuals, and generative design. Therefore, c2.js can also be integrated into a JavaScript library.

In this context, a tool like esm.sh can be especially useful. esm.sh acts as a CDN that converts npm packages into ES modules, making them easier to import directly into your JavaScript projects without extra bundling. This is ideal when working with modern development environments like Deno or writing JavaScript modules that need clean, importable packages. So, if one of the libraries you’re using doesn’t natively support ES modules, esm.sh helps bridge that gap, making integration smoother and more modular-friendly.

<!-- Make sure to include p5.js in your blog -->
<script src="https://cdn.jsdelivr.net/npm/p5@1.6.0/lib/p5.min.js"></script>
<script>
  let t = 0;

  function setup() {
    createCanvas(400, 400);
    noStroke();
  }

  function draw() {
    background(255, 240, 200);

    // Simulate a signal/envelope using sin(t)
    let envelope = sin(t) * 50 + 100; // Value oscillates between 50 and 150

    fill(255, 105, 180, 150); // pink with some transparency
    ellipse(width / 2, height / 2, envelope); // diameter controlled by envelope

    t += 0.05; // Increment time
  }
</script>

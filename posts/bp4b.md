---
title: Glitch, Net Art, & Intermediate JS
published_at: 2025-04-01
snippet: Week 4b
disable_html_sanitization: true
allow_math: true
---

<canvas id="self_portrait"></canvas>

  <script type="module">

    const cnv = document.getElementById('self_portrait');
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = cnv.width * 9 / 16;
    cnv.style.backgroundColor = 'deeppink';

    const ctx = cnv.getContext('2d');

    let img_data;

    const draw = (i) => ctx.drawImage(i, 0, 0, cnv.width, cnv.height);

    const img = new Image();
    img.crossOrigin = 'anonymous'; 
    img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width);
      draw(img);
      img_data = cnv.toDataURL("image/jpeg");
      add_glitch();
    };

  
    img.src = '/self_portrait.jpg';

    const rand_int = (max) => Math.floor(Math.random() * max);

    const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int(chunk_max / 4) * 4;
      const i = rand_int(data.length - 24 - chunk_size) + 24;
      const front = data.slice(0, i);
      const back = data.slice(i + chunk_size);
      const result = front + back;
      return repeats === 0 ? result : glitchify(result, chunk_max, repeats - 1);
    };

    const glitch_arr = [];

    const add_glitch = () => {
      const i = new Image();
      i.onload = () => {
        glitch_arr.push(i);
        if (glitch_arr.length < 12) {
          add_glitch();
        } else {
          draw_frame();
        }
      };
      i.src = glitchify(img_data, 96, 6);
    };

    let is_glitching = false;
    let glitch_i = 0;

    const draw_frame = () => {
      if (is_glitching) draw(glitch_arr[glitch_i]);
      else draw(img);

      const prob = is_glitching ? 0.05 : 0.02;
      if (Math.random() < prob) {
        glitch_i = rand_int(glitch_arr.length);
        is_glitching = !is_glitching;
      }

      requestAnimationFrame(draw_frame);
    };

  </script>

</body>
</html>

```js
//canvas element that draws the self portrait.
<canvas id="self_portrait"></canvas>

  <script type="module">
//gets the refrence to the canvas
    const cnv = document.getElementById('self_portrait');

//set the dimentions to fit 16:9 aspect ratio.
    cnv.width = cnv.parentNode.scrollWidth;
    cnv.height = cnv.width * 9 / 16;
    cnv.style.backgroundColor = 'deeppink';

// gets a 2D drawing context
    const ctx = cnv.getContext('2d');

// will store the image for glitching
    let img_data;

// function to draw an image onto the canvas
    const draw = (i) => ctx.drawImage(i, 0, 0, cnv.width, cnv.height);

//loads the source image
    const img = new Image();
    img.crossOrigin = 'anonymous';
    img.onload = () => {
      cnv.height = cnv.width * (img.height / img.width);

//draws the orginal image
      draw(img);

 // converts canvas image to string for glitch
      img_data = cnv.toDataURL("image/jpeg");

 // starts the glich generation.
      add_glitch();
    };

// image file path
    img.src = '/self_portrait.jpg';

// return a random integer between 0 and max
    const rand_int = (max) => Math.floor(Math.random() * max);

//Glitch function that randomly chops out chunks of image data as a string
    const glitchify = (data, chunk_max, repeats) => {
      const chunk_size = rand_int(chunk_max / 4) * 4; // keeps chunks as multiples of 4
      const i = rand_int(data.length - 24 - chunk_size) + 24;//skips header
      const front = data.slice(0, i);
      const back = data.slice(i + chunk_size);
      const result = front + back;
      return repeats === 0 ? result : glitchify(result, chunk_max, repeats - 1);
    };

//stores glitched image variants
    const glitch_arr = [];

//generating multiple glitched images recursively
    const add_glitch = () => {
      const i = new Image();
      i.onload = () => {
        glitch_arr.push(i);
        if (glitch_arr.length < 12) {
          add_glitch();//keeps generating
        } else {
          draw_frame();//starts animation loop
        }
      };
      //applies 6 glitches
      i.src = glitchify(img_data, 96, 6);
    };

//controls whether to display glitched image
        let is_glitching = false;
        let glitch_i = 0; // index of current glitched image

//animation loop that toggles between clean and glitched image
    const draw_frame = () => {
      if (is_glitching) draw(glitch_arr[glitch_i]);
      else draw(img);

//math probability switching states
      const prob = is_glitching ? 0.05 : 0.02;
      if (Math.random() < prob) {
        glitch_i = rand_int(glitch_arr.length); // pick a new glitch frame
        is_glitching = !is_glitching;
      }

// keeps looping
      requestAnimationFrame(draw_frame);
    };

  </script>

</body>
</html>

```

<div style="height: 100px;"></div>

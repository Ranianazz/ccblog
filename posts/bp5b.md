---
title: Three.js
published_at: 2025-04-04
snippet: Week 5b
disable_html_sanitization: true
allow_math: true
---

<!DOCTYPE html>
<html lang="en">
<head>
  <title>three.js webgl - morph targets - horse</title>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0" />
  <link type="text/css" rel="stylesheet" href="main.css" />
  <style>
    body {
      background-color: #f0f0f0;
      color: #444;
      font-family: sans-serif;
      margin: 0;
      padding: 2rem;
    }

    a {
    color: #08f;
    }

    #info {
    text-align: center;
    margin-bottom: 1rem;
    }

    /* 16:9 container with max-width, centered */
    #threejs-container {
    position: relative;
    width: 100%;
    max-width: 960px;
    margin: 0 auto;
    padding: 1rem;
    border: 1px solid #ddd;
    background: #fff;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    overflow: hidden;
    aspect-ratio: 16 / 9; /* Maintains 16:9 ratio */
    }

    canvas {
    position: absolute;
    top: 0;
    left: 0;
    width: 100% !important;
    height: 100% !important;
    display: block;
    }

  </style>
</head>
<body>

  <div id="info">
    <a href="https://threejs.org" target="_blank" rel="noopener">three.js</a> webgl - morph targets - horse<br />
    model by <a href="https://mirada.com/" target="_blank" rel="noopener">mirada</a> from <a href="http://www.ro.me" target="_blank" rel="noopener">rome</a>
  </div>

  <!-- Styled container with 16:9 aspect ratio -->
  <div id="threejs-container"></div>

  <script type="importmap">
    {
      "imports": {
        "three": "/250408/build/three.module.js",
        "three/Jsm/": "./jsm/"
      }
    }
  </script>

  <script type="module">
    import * as THREE from 'three';
    import Stats from '/250408/jsm/libs/stats.module.js';
    import { GLTFLoader } from '/250408/jsm/loaders/GLTFLoader.js';

    let container, stats;
    let camera, scene, renderer;
    let mesh, mixer;

    const radius = 600;
    let theta = 0;
    let prevTime = Date.now();

    init();

    function init() {
      container = document.getElementById('threejs-container');

      camera = new THREE.PerspectiveCamera(50, 16 / 9, 1, 10000);
      camera.position.y = 300;

      scene = new THREE.Scene();
      scene.background = new THREE.Color(0xffffff);

      const light1 = new THREE.DirectionalLight(0xefefff, 5);
      light1.position.set(1, 1, 1).normalize();
      scene.add(light1);

      const light2 = new THREE.DirectionalLight(0xffefef, 5);
      light2.position.set(-1, -1, -1).normalize();
      scene.add(light2);

      const loader = new GLTFLoader();
      loader.load('/250408/models/gltf/Horse.glb', function (gltf) {
        mesh = gltf.scene.children[0];
        mesh.scale.set(1.5, 1.5, 1.5);
        scene.add(mesh);

        mixer = new THREE.AnimationMixer(mesh);
        mixer.clipAction(gltf.animations[0]).setDuration(1).play();
      });

      renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setPixelRatio(window.devicePixelRatio);
      renderer.setSize(container.clientWidth, container.clientHeight);
      renderer.setAnimationLoop(animate);
      container.appendChild(renderer.domElement);

      stats = new Stats();
      container.appendChild(stats.dom);

      window.addEventListener('resize', onWindowResize);
    }

    function onWindowResize() {
      const width = container.clientWidth;
      const height = container.clientHeight;

      camera.aspect = width / height;
      camera.updateProjectionMatrix();

      renderer.setSize(width, height);
    }

    function animate() {
      render();
      stats.update();
    }

    function render() {
      theta += 0.1;

      camera.position.x = radius * Math.sin(THREE.MathUtils.degToRad(theta));
      camera.position.z = radius * Math.cos(THREE.MathUtils.degToRad(theta));
      camera.lookAt(0, 150, 0);

      if (mixer) {
        const time = Date.now();
        mixer.update((time - prevTime) * 0.001);
        prevTime = time;
      }

      renderer.render(scene, camera);
    }
  </script>
</body>
</html>

Sabato Visconti's artworks convey a sense of distortion, transforming a beautiful flower into a chaotic, unrecognizable shape. This exemplifies post-digital art, where the real and surreal collide, challenging our perception of reality. Rather than presenting the true form of the flower, the artwork immerses it in a false reality, making it difficult to recognize its original beauty.

Under the hood Sabato Visconti utilises the function ‘sin’ to create sinusoids to render the Under the hood, Sabato Visconti uses the ‘sin’ function to generate sinusoids, which introduces rhythmic, wave-like distortions to the image data. These calculated distortions warp the polygons, bending and merging them into a rotational polynormal—an abstract, fluid form that resists traditional geometry. The result is a digital mutation, where structure and chaos blend, echoing the tension between organic beauty and algorithmic manipulation.

<div style="height: 100px;"></div>

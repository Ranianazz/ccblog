---
title: JavaScript Ecology Libraries, Packages, & Modules
published_at: 2025-04-04
snippet: Week 5a
disable_html_sanitization: true
allow_math: true
---

# q5.js

q5.js is a beginner-friendly learning library that is compatible with p5.js. There are many clubs to join that serve as learning platforms, covering a wide range of genres from apps and software to comedy and illustration.

c2.js is similar to q5.js; however, it is primarily based on a JavaScript library for creative coding. It utilises geometric shapes, simulations, algorithms, and other modules to create digital interactive artworks.

SVG.js is a platform that uses code to create animated images. It offers a faster and more efficient method of coding, as it is easier to read and requires less code to animate an image.

<!DOCTYPE html>
<html lang="en">
	<head>
		<title>three.js webgl - effects - anaglyph</title>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, user-scalable=no, minimum-scale=1.0, maximum-scale=1.0">
		<link type="text/css" rel="stylesheet" href="main.css">
	</head>
	<body>
		<div id="info">
			<a href="https://threejs.org" target="_blank" rel="noopener">three.js</a> - effects - anaglyph<br/>
			skybox by <a href="https://www.pauldebevec.com/" target="_blank" rel="noopener">Paul Debevec</a>
		</div>

<script type="importmap">
{
    "imports": {
	"three": "../build/three.module.js",
	"three/addons/": "./jsm/"
	}
}
		</script>

<script type="module">

			import * as THREE from 'three';

			import { AnaglyphEffect } from 'three/addons/effects/AnaglyphEffect.js';

			let container, camera, scene, renderer, effect;

			const spheres = [];

			let mouseX = 0;
			let mouseY = 0;

			let windowHalfX = window.innerWidth / 2;
			let windowHalfY = window.innerHeight / 2;

			document.addEventListener( 'mousemove', onDocumentMouseMove );

			init();

			function init() {

				container = document.createElement( 'div' );
				document.body.appendChild( container );

				camera = new THREE.PerspectiveCamera( 60, window.innerWidth / window.innerHeight, 0.01, 100 );
				camera.position.z = 3;

				const path = 'textures/cube/pisa/';
				const format = '.png';
				const urls = [
					path + 'px' + format, path + 'nx' + format,
					path + 'py' + format, path + 'ny' + format,
					path + 'pz' + format, path + 'nz' + format
				];

				const textureCube = new THREE.CubeTextureLoader().load( urls );

				scene = new THREE.Scene();
				scene.background = textureCube;

				const geometry = new THREE.SphereGeometry( 0.1, 32, 16 );
				const material = new THREE.MeshBasicMaterial( { color: 0xffffff, envMap: textureCube } );

				for ( let i = 0; i < 500; i ++ ) {

					const mesh = new THREE.Mesh( geometry, material );

					mesh.position.x = Math.random() * 10 - 5;
					mesh.position.y = Math.random() * 10 - 5;
					mesh.position.z = Math.random() * 10 - 5;

					mesh.scale.x = mesh.scale.y = mesh.scale.z = Math.random() * 3 + 1;

					scene.add( mesh );

					spheres.push( mesh );

				}

				//

				renderer = new THREE.WebGLRenderer();
				renderer.setPixelRatio( window.devicePixelRatio );
				renderer.setAnimationLoop( animate );
				container.appendChild( renderer.domElement );

				const width = window.innerWidth || 2;
				const height = window.innerHeight || 2;

				effect = new AnaglyphEffect( renderer );
				effect.setSize( width, height );

				//

				window.addEventListener( 'resize', onWindowResize );

			}

			function onWindowResize() {

				windowHalfX = window.innerWidth / 2;
				windowHalfY = window.innerHeight / 2;

				camera.aspect = window.innerWidth / window.innerHeight;
				camera.updateProjectionMatrix();

				effect.setSize( window.innerWidth, window.innerHeight );

			}

			function onDocumentMouseMove( event ) {

				mouseX = ( event.clientX - windowHalfX ) / 100;
				mouseY = ( event.clientY - windowHalfY ) / 100;

			}

			//

			function animate() {

				render();

			}

			function render() {

				const timer = 0.0001 * Date.now();

				camera.position.x += ( mouseX - camera.position.x ) * .05;
				camera.position.y += ( - mouseY - camera.position.y ) * .05;

				camera.lookAt( scene.position );

				for ( let i = 0, il = spheres.length; i < il; i ++ ) {

					const sphere = spheres[ i ];

					sphere.position.x = 5 * Math.cos( timer + i );
					sphere.position.y = 5 * Math.sin( timer + i * 1.1 );

				}

				effect.render( scene, camera );

			}

		</script>

</body>
</html>

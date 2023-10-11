<template>
  <div id="three-container"></div>
</template>

<script>
import * as THREE from "three";
import { GLTFLoader } from "three/addons/loaders/GLTFLoader.js";

export default {
  mounted() {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.getElementById("three-container").appendChild(renderer.domElement);

    camera.position.z =8;

    // Create an ambient light
    const ambientLight = new THREE.AmbientLight(0xffffff);
    scene.add(ambientLight);

    // Create the GLTFLoader
    const loader = new GLTFLoader();

    // Load the GLTF model
    loader.load("./sr5.gltf", (gltf) => {
      // After loading, you can access the loaded model
      const model = gltf.scene;

      // Optionally, you can scale, position, or manipulate the model
      model.scale.set(50, 50, 50);

      // Add the model to the scene
      scene.add(model);
      model.position.y -= 1;
      // Animation function
      const animate = () => {
        requestAnimationFrame(animate);

        // Rotate the model or perform other animations
        model.rotation.y += 0.001;


        renderer.render(scene, camera);
      };

      animate();
    });
  },
};
</script>

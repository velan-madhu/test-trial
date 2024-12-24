<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Model Viewer</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: #f0f0f0; /* Optional */
        }
        #container {
            width: 100vw;
            height: 100vh;
        }
    </style>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/loaders/GLTFLoader.js"></script>
</head>
<body>
    <div id="container"></div>
    <script>
        // Create scene, camera, and renderer
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.getElementById('container').appendChild(renderer.domElement);

        // Add ambient light (soft, global lighting)
        const ambientLight = new THREE.AmbientLight(0x404040, 2); // Soft light
        scene.add(ambientLight);

        // Add directional light (strong, focused lighting)
        const directionalLight = new THREE.DirectionalLight(0xffffff, 1.5);
        directionalLight.position.set(5, 5, 5); // Position the light
        directionalLight.castShadow = true; // Enable shadows if needed
        scene.add(directionalLight);

        // Load the GLB model
        const loader = new THREE.GLTFLoader();
        loader.load(
            './public/assets/New-Year-Wishes-AR.glb', 
            function (gltf) {
                const model = gltf.scene;
                model.scale.set(1, 1, 1); // Adjust scale if the model is too large or small
                model.position.set(0, 0, 0); // Center the model in the scene
                scene.add(model);
            },
            undefined,
            function (error) {
                console.error('Error loading model:', error);
            }
        );

        // Camera position and animation loop
        camera.position.set(3, 3, 7); // Adjusted camera position to better view the model
        function animate() {
            requestAnimationFrame(animate);
            renderer.render(scene, camera);
        }
        animate();

        // Handle window resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>

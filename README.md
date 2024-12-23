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

        // Add a subtle ambient light to light up all objects
        const ambientLight = new THREE.AmbientLight(0x404040, 2); // Soft white light
        scene.add(ambientLight);

        // Add a directional light for stronger illumination
        const directionalLight = new THREE.DirectionalLight(0xffffff, 1.5);
        directionalLight.position.set(5, 5, 5); // Adjust position for better shadows
        directionalLight.castShadow = true; // Enable shadows
        scene.add(directionalLight);

        // Add helper for debugging light positions (optional)
        const lightHelper = new THREE.DirectionalLightHelper(directionalLight, 1);
        scene.add(lightHelper);

        // Load the GLB model
        const loader = new THREE.GLTFLoader();
        loader.load(
            './public/assets/New-Year-Wishes-AR.glb',
            function (gltf) {
                // Scale and position the model as needed
                const model = gltf.scene;
                model.scale.set(1, 1, 1); // Adjust scale
                model.position.set(0, 0, 0); // Center model
                scene.add(model);
            },
            undefined,
            function (error) {
                console.error('Error loading model:', error);
            }
        );

        // Position the camera
        camera.position.set(2, 2, 5); // Adjusted for a better view of the model

        // Animation loop
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

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

        // Add ambient light
        const ambientLight = new THREE.AmbientLight(0x404040, 2); // Soft white light
        scene.add(ambientLight);

        // Add directional light
        const directionalLight = new THREE.DirectionalLight(0xffffff, 1.5);
        directionalLight.position.set(5, 5, 5);
        directionalLight.castShadow = true;
        scene.add(directionalLight);

        // Load the GLB model
        const loader = new THREE.GLTFLoader();
        loader.load(
            './New-Year-Wishes-AR.glb', // Ensure the path matches your setup
            function (gltf) {
                const model = gltf.scene;

                // Set model position and scale
                model.scale.set(1, 1, 1);
                model.position.set(0, 0, 0);

                // Traverse model to ensure proper rendering
                model.traverse((node) => {
                    if (node.isMesh) {
                        node.castShadow = true;
                        node.receiveShadow = true;

                        // Check for materials and enable proper rendering
                        if (node.material) {
                            node.material.metalness = 0; // Adjust if metallic look is causing artifacts
                            node.material.roughness = 0.5; // Tune roughness for smooth visuals
                        }
                    }
                });

                scene.add(model);
            },
            undefined,
            function (error) {
                console.error('Error loading model:', error);
            }
        );

        // Camera position
        camera.position.set(3, 3, 7); // Adjust for better framing

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

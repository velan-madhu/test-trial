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
            background-color: #f0f0f0;
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
        const scene = new THREE.Scene();
        const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.getElementById('container').appendChild(renderer.domElement);

        // Lights
        const ambientLight = new THREE.AmbientLight(0x404040, 5);
        scene.add(ambientLight);

        const directionalLight = new THREE.DirectionalLight(0xffffff, 5);
        directionalLight.position.set(5, 5, 5);
        scene.add(directionalLight);

        // Grid Helper
        const gridHelper = new THREE.GridHelper(10, 10);
        scene.add(gridHelper);

        // Load GLB Model
        const loader = new THREE.GLTFLoader();
        loader.load(
            './public/assets/New-Year-Wishes-AR.glb', 
            function (gltf) {
                console.log("Model Loaded Successfully:", gltf);
                const model = gltf.scene;
                model.scale.set(1, 1, 1);
                model.position.set(0, 0, 0);
                scene.add(model);
            },
            function (xhr) {
                console.log((xhr.loaded / xhr.total) * 100 + '% loaded');
            },
            function (error) {
                console.error('Error loading model:', error);
            }
        );

        // Add a Cube for Testing
        const geometry = new THREE.BoxGeometry();
        const material = new THREE.MeshStandardMaterial({ color: 0x00ff00 });
        const cube = new THREE.Mesh(geometry, material);
        cube.position.set(0, 0, -2); // Test Position
        scene.add(cube);

        // Camera and Animation Loop
        camera.position.set(0, 2, 5);
        camera.lookAt(0, 0, 0);

        function animate() {
            requestAnimationFrame(animate);
            renderer.render(scene, camera);
        }
        animate();

        // Handle Window Resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>

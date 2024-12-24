<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GLB Viewer</title>
    <script type="module" src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"></script>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        model-viewer {
            width: 100%;
            height: 100%;
        }
    </style>
</head>
<body>
    <model-viewer 
        src="./public/assets/New-Year-Wishes-AR.glb" 
        alt="A 3D model" 
        auto-rotate 
        camera-controls 
        background-color="#ffffff">
    </model-viewer>
</body>
</html>

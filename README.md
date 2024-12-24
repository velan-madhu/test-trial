<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Improved GLB Viewer</title>
    <script type="module" src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"></script>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0; /* Light background color */
        }
        model-viewer {
            width: 80%; /* Adjust size as needed */
            height: 80%; /* Adjust size as needed */
            background-color: transparent; /* Make model-viewer background transparent */
        }
    </style>
</head>
<body>
    <model-viewer 
             src="https://create.overlyapp.com/webar/7a5d4d3080557d91726d3a96199b17ff07e852d3"
<!--         src="./public/assets/New-Year-Wishes-AR.glb"  -->
        alt="A 3D model" 
        auto-rotate 
        camera-controls 
        ar 
        environment-image="neutral" 
        exposure="1" 
        skybox-image=""
        shadow-intensity="1">
    </model-viewer>
</body>
</html>

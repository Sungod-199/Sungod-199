<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aiming Training App</title>
    <style>
        canvas { border: 1px solid black; }
    </style>
</head>
<body>
    <h1>Aiming Training App</h1>
    <canvas id="trainingCanvas" width="800" height="600"></canvas>
    <script>
        const canvas = document.getElementById('trainingCanvas');
        const ctx = canvas.getContext('2d');

        function drawTarget(x, y, size) {
            ctx.beginPath();
            ctx.arc(x, y, size, 0, Math.PI * 2);
            ctx.fillStyle = '#ff0000'; // Target color
            ctx.fill();
            ctx.closePath();
        }

        function clearCanvas() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        function startTraining() {
            let targetX = Math.random() * canvas.width;
            let targetY = Math.random() * canvas.height;
            let targetSize = 30;

            function update() {
                clearCanvas();
                drawTarget(targetX, targetY, targetSize);
                requestAnimationFrame(update);
            }

            update();

            canvas.addEventListener('click', (e) => {
                const rect = canvas.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const y = e.clientY - rect.top;

                const dx = x - targetX;
                const dy = y - targetY;
                if (Math.sqrt(dx * dx + dy * dy) < targetSize) {
                    alert('Hit!');
                } else {
                    alert('Miss!');
                }
            });
        }

        startTraining();
    </script>
</body>
</html>

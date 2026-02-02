<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Code-Only Garden</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            background: linear-gradient(#a2d2ff, #fef9e7);
            overflow: hidden;
            font-family: 'Arial', sans-serif;
            cursor: crosshair;
        }

        /* UI Overlay */
        .info {
            position: absolute;
            top: 20px;
            width: 100%;
            text-align: center;
            color: #5b7065;
            pointer-events: none;
        }

        /* The Flower SVG Styling */
        .flower {
            position: absolute;
            width: 60px;
            height: 60px;
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
            transform-origin: center bottom;
        }

        @keyframes popIn {
            0% { transform: scale(0) rotate(0deg); }
            100% { transform: scale(1) rotate(10deg); }
        }

        /* Butterfly Styling */
        #butterfly {
            position: absolute;
            width: 40px;
            pointer-events: none;
            z-index: 100;
            transition: transform 0.2s ease-out;
        }

        /* Ground */
        .ground {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 15vh;
            background: #95d5b2;
            z-index: 5;
        }
    </style>
</head>
<body onclick="createFlower(event)">

    <div class="info">
        <h1>Our Digital Greenhouse</h1>
        <p>Click the ground to grow a memory</p>
    </div>

    <svg id="butterfly" viewBox="0 0 50 50">
        <path fill="#ffafcc" d="M25 25 Q10 10 5 20 Q5 30 25 25 Q40 10 45 20 Q45 30 25 25">
            <animateTransform attributeName="transform" type="scale" values="1 1; 0.8 1; 1 1" dur="0.2s" repeatCount="indefinite" />
        </path>
    </svg>

    <div class="ground"></div>

    <script>
        const colors = ['#ff87ab', '#ffb3c1', '#fb6f92', '#c1121f', '#ffccd5'];
        
        function createFlower(e) {
            const color = colors[Math.floor(Math.random() * colors.length)];
            
            // Create a Flower using Pure SVG Code
            const flowerSVG = `
                <svg class="flower" viewBox="0 0 100 100" style="left:${e.clientX - 30}px; top:${e.clientY - 50}px">
                    <path d="M50 100 Q60 80 50 50" stroke="#2d6a4f" stroke-width="4" fill="none" />
                    <circle cx="50" cy="35" r="15" fill="${color}" />
                    <circle cx="35" cy="50" r="15" fill="${color}" />
                    <circle cx="65" cy="50" r="15" fill="${color}" />
                    <circle cx="50" cy="65" r="15" fill="${color}" />
                    <circle cx="50" cy="50" r="8" fill="#ffeb3b" />
                </svg>
            `;
            
            document.body.insertAdjacentHTML('beforeend', flowerSVG);
        }

        // Butterfly Movement
        const bfly = document.getElementById('butterfly');
        document.addEventListener('mousemove', (e) => {
            bfly.style.left = e.clientX + 'px';
            bfly.style.top = e.clientY + 'px';
        });
    </script>
</body>
</html>

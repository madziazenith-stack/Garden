<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sparkling Digital Garden</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            background: linear-gradient(#1a2a6c, #b21f1f, #fdbb2d); /* A romantic sunset gradient */
            overflow: hidden;
            font-family: 'Georgia', serif;
            cursor: crosshair;
        }

        .info {
            position: absolute;
            top: 30px;
            width: 100%;
            text-align: center;
            color: white;
            pointer-events: none;
            text-shadow: 0 0 10px rgba(0,0,0,0.5);
            z-index: 10;
        }

        /* Flower Container */
        .flower-wrapper {
            position: absolute;
            width: 80px;
            height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: transform 0.3s ease;
        }

        .flower-wrapper:hover {
            transform: scale(1.2);
        }

        /* The Flower SVG */
        .flower-svg {
            width: 100%;
            height: 100%;
            filter: drop-shadow(0 0 5px rgba(255,255,255,0.3));
            animation: grow 0.6s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }

        @keyframes grow {
            0% { transform: scale(0); }
            100% { transform: scale(1); }
        }

        /* Sparkle/Pulse effect on hover */
        .flower-wrapper:hover .flower-svg {
            filter: drop-shadow(0 0 15px #fff);
            animation: pulse 1s infinite alternate;
        }

        @keyframes pulse {
            from { transform: scale(1); }
            to { transform: scale(1.1); }
        }

        /* Heart Particles */
        .heart-particle {
            position: absolute;
            color: #ff4d6d;
            font-size: 20px;
            pointer-events: none;
            animation: floatUp 1.5s ease-out forwards;
            z-index: 100;
        }

        @keyframes floatUp {
            0% { transform: translateY(0) scale(1); opacity: 1; }
            100% { transform: translateY(-100px) translateX(20px) scale(0); opacity: 0; }
        }

        #butterfly {
            position: absolute;
            width: 40px;
            pointer-events: none;
            z-index: 1000;
            filter: drop-shadow(0 0 10px gold);
        }

        .ground {
            position: absolute;
            bottom: 0;
            width: 100%;
            height: 10vh;
            background: rgba(45, 106, 79, 0.3);
            backdrop-filter: blur(5px);
        }
    </style>
</head>
<body onclick="plantFlower(event)">

    <div class="info">
        <h1>Our Sparkling Garden</h1>
        <p>Plant a flower and hover over it to see it sparkle...</p>
    </div>

    <svg id="butterfly" viewBox="0 0 50 50">
        <path fill="#ffd700" d="M25 25 Q10 10 5 20 Q5 30 25 25 Q40 10 45 20 Q45 30 25 25">
            <animateTransform attributeName="transform" type="scale" values="1 1; 0.7 1; 1 1" dur="0.15s" repeatCount="indefinite" />
        </path>
    </svg>

    <div class="ground"></div>

    <script>
        const flowerColors = ['#ff0054', '#ff5400', '#ffbd00', '#9ef01a', '#00f5d4', '#00bbf9', '#9b5de5'];

        function plantFlower(e) {
            // Prevent planting too high up
            if(e.clientY < 100) return;

            const color = flowerColors[Math.floor(Math.random() * flowerColors.length)];
            const wrapper = document.createElement('div');
            wrapper.className = 'flower-wrapper';
            wrapper.style.left = (e.clientX - 40) + 'px';
            wrapper.style.top = (e.clientY - 40) + 'px';

            wrapper.innerHTML = `
                <svg class="flower-svg" viewBox="0 0 100 100">
                    <circle cx="50" cy="30" r="15" fill="${color}" />
                    <circle cx="30" cy="50" r="15" fill="${color}" />
                    <circle cx="70" cy="50" r="15" fill="${color}" />
                    <circle cx="50" cy="70" r="15" fill="${color}" />
                    <circle cx="50" cy="50" r="10" fill="yellow" />
                </svg>
            `;

            // Add heart sparkle trigger
            wrapper.onmouseover = () => {
                for(let i=0; i<5; i++) {
                    createHeart(e.clientX, e.clientY);
                }
            };

            document.body.appendChild(wrapper);
        }

        function createHeart(x, y) {
            const heart = document.createElement('div');
            heart.className = 'heart-particle';
            heart.innerHTML = '❤️';
            // Randomize position slightly around the flower
            heart.style.left = (x - 10 + (Math.random() * 20)) + 'px';
            heart.style.top = (y - 10) + 'px';
            
            document.body.appendChild(heart);
            setTimeout(() => heart.remove(), 1500);
        }

        // Butterfly follow
        const bfly = document.getElementById('butterfly');
        document.addEventListener('mousemove', (e) => {
            bfly.style.left = (e.clientX - 20) + 'px';
            bfly.style.top = (e.clientY - 20) + 'px';
        });
    </script>
</body>
</html>

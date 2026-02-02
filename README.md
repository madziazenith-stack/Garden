<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Our Digital Garden</title>
    <style>
        :root {
            --grass: #a8e6cf;
            --flower-1: #ff8b94;
            --flower-2: #ffd3b6;
            --flower-3: #dcedc1;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            background: linear-gradient(to bottom, #e0f7fa 0%, #a8e6cf 100%);
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            cursor: url('https://cdn-icons-png.flaticon.com/32/427/427735.png'), auto;
        }

        #garden-ui {
            position: absolute;
            top: 20px;
            width: 100%;
            text-align: center;
            z-index: 10;
            pointer-events: none;
        }

        h1 { color: #5d8a66; text-shadow: 2px 2px white; margin-bottom: 5px; }
        p { color: #6a9c78; font-style: italic; }

        .flower {
            position: absolute;
            width: 40px;
            height: 40px;
            transform-origin: bottom center;
            animation: grow 1s ease-out forwards, sway 3s ease-in-out infinite;
            cursor: pointer;
        }

        /* The Petals */
        .flower::before {
            content: '🌸'; /* You can alternate these with JS */
            font-size: 30px;
            display: block;
        }

        /* The Tooltip (The Memory) */
        .flower:hover::after {
            content: attr(data-memory);
            position: absolute;
            bottom: 50px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(255, 255, 255, 0.9);
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 14px;
            color: #d81b60;
            white-space: nowrap;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            z-index: 100;
        }

        @keyframes grow {
            0% { transform: scale(0) rotate(0deg); }
            100% { transform: scale(1) rotate(0deg); }
        }

        @keyframes sway {
            0%, 100% { transform: rotate(-5deg); }
            50% { transform: rotate(5deg); }
        }

        .butterfly {
            position: absolute;
            font-size: 20px;
            pointer-events: none;
            transition: all 0.5s ease-out;
            z-index: 50;
        }
    </style>
</head>
<body onclick="plantFlower(event)">

    <div id="garden-ui">
        <h1>Our Memory Garden</h1>
        <p>Click anywhere to plant a memory...</p>
    </div>

    <div id="butterfly" class="butterfly">🦋</div>

    <script>
        const memories = [
            "The day we first met ❤️",
            "That rainy evening coffee ☕",
            "When you wore that blue shirt 👕",
            "Our first long walk 🌙",
            "The way you laugh at bad jokes 😂",
            "Your favorite song playing in the car 🎵",
            "The sunset at the beach 🌅",
            "Just thinking of you right now... ✨"
        ];

        const flowerTypes = ['🌸', '🌺', '🌷', '🌻', '🌼'];

        function plantFlower(e) {
            // Don't plant if clicking on UI
            if (e.target.id === 'garden-ui') return;

            const flower = document.createElement('div');
            flower.className = 'flower';
            
            // Randomly pick a flower look and a memory
            const randomType = flowerTypes[Math.floor(Math.random() * flowerTypes.length)];
            const randomMemory = memories[Math.floor(Math.random() * memories.length)];
            
            flower.style.left = (e.clientX - 20) + 'px';
            flower.style.top = (e.clientY - 20) + 'px';
            flower.style.setProperty('--flower-emoji', `"${randomType}"`);
            flower.setAttribute('data-memory', randomMemory);
            
            // Apply the emoji via innerHTML for simplicity
            flower.innerHTML = `<span style="font-size: 40px;">${randomType}</span>`;

            document.body.appendChild(flower);
        }

        // Butterfly follow logic
        const butterfly = document.getElementById('butterfly');
        document.addEventListener('mousemove', (e) => {
            butterfly.style.left = (e.clientX + 20) + 'px';
            butterfly.style.top = (e.clientY - 20) + 'px';
        });
    </script>
</body>
</html>

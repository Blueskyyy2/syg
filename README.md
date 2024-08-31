<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Birthday Surprise</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: url('https://images.unsplash.com/photo-1506748686214-e9df14d4d9d0') no-repeat center center fixed;
            background-size: cover;
        }
        .balloon-container {
            position: relative;
            width: 100vw;
            height: 100vh;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .balloon {
            width: 60px;
            height: 80px;
            border-radius: 50%;
            position: absolute;
            cursor: pointer;
            transition: transform 0.2s;
            animation: float 6s infinite ease-in-out;
        }
        .balloon::after {
            content: '';
            width: 4px;
            height: 20px;
            background-color: inherit;
            position: absolute;
            bottom: -20px;
            left: 50%;
            transform: translateX(-50%);
        }
        .balloon:active {
            transform: scale(0.8);
        }
        @keyframes float {
            0% {
                transform: translateY(0) rotate(0deg);
            }
            50% {
                transform: translateY(-50px) rotate(15deg);
            }
            100% {
                transform: translateY(0) rotate(0deg);
            }
        }
        #cake {
            display: none;
            width: 200px;
            height: 300px;
            background: url('https://example.com/pink-cake-with-candle.png') no-repeat center center;
            background-size: contain;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
        #presentBox {
            display: none;
            width: 200px;
            height: 200px;
            background-color: #ffcc00;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            border-radius: 10px;
            cursor: pointer;
            text-align: center;
            line-height: 200px;
            font-size: 18px;
            color: black;
        }
        #music {
            display: none;
        }
    </style>
</head>
<body>
    <div class="balloon-container" id="balloon-container">
        <!-- Balon akan di-generate oleh JavaScript -->
    </div>

    <div id="cake"></div>

    <div id="presentBox" onclick="openPresent()">Open the present!</div>

    <audio id="music" autoplay loop>
        <source src="https://example.com/happy-birthday.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>

    <script>
        // Warna balon
        const colors = ['#ff6347', '#ffcc00', '#66ccff', '#cc66ff', '#99ff99', '#ff66b2', '#ff9966'];
        const container = document.getElementById('balloon-container');

        // Generate 21 balloons
        for (let i = 0; i < 21; i++) {
            const balloon = document.createElement('div');
            balloon.classList.add('balloon');
            balloon.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
            balloon.style.left = `${Math.random() * 80}vw`;
            balloon.style.top = `${Math.random() * 80}vh`;
            balloon.style.animationDuration = `${Math.random() * 2 + 4}s`;
            balloon.onclick = popBalloon;
            container.appendChild(balloon);
        }

        function popBalloon(event) {
            event.target.style.display = 'none';
            const remainingBalloons = document.querySelectorAll('.balloon:not([style*="display: none"])');
            if (remainingBalloons.length === 0) {
                showCake();
            }
        }

        function showCake() {
            const cake = document.getElementById('cake');
            cake.style.display = 'block';

            // Simulate candle blowing after 10 seconds
            setTimeout(() => {
                cake.style.background = 'url("https://example.com/extinguished-cake.png") no-repeat center center';
                cake.style.backgroundSize = 'contain';
                showPresent();
            }, 10000); // 10 seconds to simulate blowing the candle
        }

        function showPresent() {
            const presentBox = document.getElementById('presentBox');
            presentBox.style.display = 'block';
        }

        function openPresent() {
            const presentBox = document.getElementById('presentBox');
            if (presentBox.innerHTML === 'Happy Birthday!') {
                presentBox.style.display = 'none';
            } else {
                presentBox.innerHTML = 'Happy Birthday!';
                presentBox.style.width = '150px';
                presentBox.style.height = '150px';
                presentBox.style.lineHeight = '150px';
                presentBox.style.fontSize = '16px';
            }
        }
    </script>
</body>
</html>

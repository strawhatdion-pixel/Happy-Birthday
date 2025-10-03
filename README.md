<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Happy Birthday!</title>
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
            min-height: 100vh;
            margin: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: 'Montserrat', sans-serif;
        }
        .card {
            background: #fff;
            border-radius: 24px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.15);
            padding: 48px 40px;
            max-width: 420px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        .confetti {
            position: absolute;
            top: 0; left: 0; right: 0; bottom: 0;
            pointer-events: none;
            z-index: 0;
        }
        h1 {
            font-family: 'Pacifico', cursive;
            font-size: 2.8em;
            color: #ff6f61;
            margin-bottom: 0.2em;
            letter-spacing: 2px;
            text-shadow: 2px 2px 8px #ffd6d6;
        }
        p {
            font-size: 1.2em;
            color: #444;
            margin-bottom: 1.5em;
        }
        .cake {
            font-size: 3em;
            margin-bottom: 0.5em;
            animation: bounce 1.2s infinite alternate;
        }
        @keyframes bounce {
            to { transform: translateY(-12px); }
        }
        .signature {
            margin-top: 2em;
            font-family: 'Pacifico', cursive;
            color: #ffb347;`
            font-size: 1.3em;
        }
    </style>
</head>
<body>
    <div class="card">
        <canvas class="confetti"></canvas>
        <div class="cake">🎂</div>
        <h1>Happy Birthday!</h1>
        <p>
            Happy Birthday Tito, I Wish you all the best.<br>
            May your year ahead sparkle with happiness and dreams come true!
        </p>
        <div class="signature">Truly yours, <br>Dion</div>
    </div>
    <script>
        // Simple confetti effect
        const canvas = document.querySelector('.confetti');
        const ctx = canvas.getContext('2d');
        let W, H;
        function resize() {
            W = canvas.width = canvas.offsetWidth = canvas.parentElement.offsetWidth;
            H = canvas.height = canvas.offsetHeight = canvas.parentElement.offsetHeight;
        }
        window.addEventListener('resize', resize);
        resize();

        const confettiCount = 60;
        const confettiColors = ['#ff6f61', '#ffb347', '#f7cac9', '#92a8d1', '#b5ead7'];
        const confetti = Array.from({length: confettiCount}, () => ({
            x: Math.random() * W,
            y: Math.random() * H,
            r: 6 + Math.random() * 8,
            d: Math.random() * confettiCount,
            color: confettiColors[Math.floor(Math.random() * confettiColors.length)],
            tilt: Math.random() * 10 - 5
        }));

        function drawConfetti() {
            ctx.clearRect(0, 0, W, H);
            confetti.forEach(c => {
                ctx.beginPath();
                ctx.ellipse(c.x, c.y, c.r, c.r/2, c.tilt, 0, 2 * Math.PI);
                ctx.fillStyle = c.color;
                ctx.fill();
            });
            updateConfetti();
        }

        function updateConfetti() {
            confetti.forEach(c => {
                c.y += Math.cos(c.d) + 1 + c.r/4;
                c.x += Math.sin(c.d) * 2;
                c.d += 0.01;
                if (c.y > H) {
                    c.y = -10;
                    c.x = Math.random() * W;
                }
            });
        }

        function animate() {
            drawConfetti();
            requestAnimationFrame(animate);
        }
        animate();
    </script>
</body>
</html>
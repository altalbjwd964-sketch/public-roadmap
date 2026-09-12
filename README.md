<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <title>Heart Landing</title>
    <style>
        body {
            margin: 0;
            background-color: #050505;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        canvas {
            position: absolute;
            top: 0;
            left: 0;
        }
    </style>
</head>
<body>

    <canvas id="heartCanvas"></canvas>

    <script>
        const canvas = document.getElementById("heartCanvas");
        const ctx = canvas.getContext("2d");

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let particles = [];
        let angle = 0;

        function heartFunction(t) {
            let x = 16 * Math.pow(Math.sin(t), 3);
            let y = -(13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t));
            return { x, y };
        }

        // إنشاء النقاط
        for (let i = 0; i < 350; i++) {
            let t = Math.random() * Math.PI * 2;
            let pos = heartFunction(t);
            let shrink = Math.random() > 0.3 ? Math.random() : 1.0;
            
            particles.push({
                baseX: pos.x * shrink,
                baseY: pos.y * shrink,
                color: ["#ff2a6d", "#ff5e7e", "#ff0055", "#e60049", "#ff99ac"][Math.floor(Math.random() * 5)],
                size: Math.floor(Math.random() * 6) + 10
            });
        }

        function animate() {
            ctx.fillStyle = "rgba(5, 5, 5, 0.3)";
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            let scale = 15;
            let pulse = 1 + 0.08 * Math.sin(angle);
            angle += 0.08;

            let centerX = canvas.width / 2;
            let centerY = canvas.height / 2;

            particles.forEach(p => {
                let currX = centerX + p.baseX * scale * pulse;
                let currY = centerY + p.baseY * scale * pulse;

                ctx.fillStyle = p.color;
                ctx.font = `bold ${p.size}px Arial`;
                ctx.fillText("I love you", currX, currY);
            });

            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>

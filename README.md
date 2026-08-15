<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>阻绝 生日快乐</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            background-size: 400% 400%;
            animation: gradientShift 8s ease infinite;
            overflow: hidden;
            font-family: 'PingFang SC', 'Microsoft YaHei', sans-serif;
            color: white;
            text-align: center;
            cursor: pointer;
            user-select: none;
        }
        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        .cake {
            font-size: 120px;
            animation: cakeFloat 3s ease-in-out infinite, cakeGlow 2s ease-in-out infinite alternate;
            filter: drop-shadow(0 0 20px rgba(255,200,0,0.8));
            margin-bottom: 30px;
        }
        @keyframes cakeFloat {
            0%, 100% { transform: translateY(0) rotate(0deg); }
            25% { transform: translateY(-20px) rotate(3deg); }
            75% { transform: translateY(-10px) rotate(-3deg); }
        }
        @keyframes cakeGlow {
            from { filter: drop-shadow(0 0 20px rgba(255,200,0,0.6)); }
            to { filter: drop-shadow(0 0 40px rgba(255,100,200,0.9)); }
        }
        h1 {
            font-size: 2.8em;
            text-shadow: 0 0 20px rgba(255,255,255,0.5);
            margin-bottom: 15px;
            opacity: 0;
            animation: fadeInUp 1s ease forwards 0.5s;
        }
        p {
            font-size: 1.5em;
            opacity: 0;
            animation: fadeInUp 1s ease forwards 1s;
        }
        .hint {
            position: fixed;
            bottom: 30px;
            font-size: 0.9em;
            opacity: 0;
            animation: fadeInUp 1s ease forwards 2s, blink 2s ease-in-out infinite 3s;
        }
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes blink {
            0%, 100% { opacity: 0.6; }
            50% { opacity: 0.2; }
        }
        /* 彩带/星星 */
        .confetti {
            position: fixed;
            top: -10px;
            width: 10px;
            height: 10px;
            border-radius: 2px;
            animation: fall linear forwards;
            pointer-events: none;
            z-index: 999;
        }
        @keyframes fall {
            to { transform: translateY(110vh) rotate(720deg); opacity: 0; }
        }
        /* 点击烟花 */
        .firework {
            position: fixed;
            width: 6px;
            height: 6px;
            border-radius: 50%;
            pointer-events: none;
            animation: explode 0.8s ease-out forwards;
            z-index: 999;
        }
        @keyframes explode {
            to { transform: translate(var(--tx), var(--ty)) scale(0); opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="cake">🎂</div>
    <h1>阻绝，生日快乐！</h1>
    <p>愿新的一岁，所求皆如愿，所行皆坦途</p>
    <div class="hint">✨ 点屏幕放烟花 ✨</div>

    <script>
        // 持续掉落彩带
        const colors = ['#ff6b6b','#ffd93d','#6bcb77','#4d96ff','#ff6eb4','#a855f7','#fff'];
        function createConfetti() {
            const el = document.createElement('div');
            el.className = 'confetti';
            el.style.left = Math.random() * 100 + 'vw';
            el.style.background = colors[Math.floor(Math.random() * colors.length)];
            el.style.width = Math.random() * 8 + 5 + 'px';
            el.style.height = Math.random() * 8 + 5 + 'px';
            el.style.animationDuration = Math.random() * 3 + 2 + 's';
            el.style.opacity = Math.random() * 0.7 + 0.3;
            document.body.appendChild(el);
            setTimeout(() => el.remove(), 5000);
        }
        setInterval(createConfetti, 200);

        // 点击放烟花
        document.body.addEventListener('click', function(e) {
            for (let i = 0; i < 12; i++) {
                const spark = document.createElement('div');
                spark.className = 'firework';
                const angle = (Math.PI * 2 / 12) * i;
                const distance = Math.random() * 80 + 40;
                spark.style.left = e.clientX + 'px';
                spark.style.top = e.clientY + 'px';
                spark.style.background = colors[Math.floor(Math.random() * colors.length)];
                spark.style.setProperty('--tx', Math.cos(angle) * distance + 'px');
                spark.style.setProperty('--ty', Math.sin(angle) * distance + 'px');
                document.body.appendChild(spark);
                setTimeout(() => spark.remove(), 800);
            }
        });
    </script>
</body>
</html>

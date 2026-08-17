<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ZD的专属纪念册</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { 
            height: 100vh; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            background: #222; 
            font-family: sans-serif; 
            overflow: hidden;
            color: #fff;
        }
        /* 书本容器 */
        .book {
            width: 90%;
            max-width: 400px;
            height: 80vh;
            position: relative;
            perspective: 1000px;
        }
        /* 每一页的通用样式 */
        .page {
            width: 100%;
            height: 100%;
            position: absolute;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
            transition: transform 0.8s ease-in-out, opacity 0.5s;
            cursor: pointer;
            user-select: none;
            padding: 20px;
        }
        /* 翻页动画控制 */
        .page.hidden-left { transform: translateX(-100%) rotateY(-20deg); opacity: 0; pointer-events: none; z-index: 1; }
        .page.hidden-right { transform: translateX(100%) rotateY(20deg); opacity: 0; pointer-events: none; z-index: 1; }
        .page.active { transform: translateX(0) rotateY(0); opacity: 1; z-index: 10; }

        /* 页面背景颜色区分 */
        .p1 { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .p2 { background: linear-gradient(to bottom, #1a2a6c, #111); }
        .p3 { background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d); }
        .p4 { background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%); color: #111; }

        /* 提示文字 */
        .hint { position: absolute; bottom: 20px; font-size: 0.9rem; opacity: 0.7; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0%, 100% { opacity: 0.4; } 50% { opacity: 1; } }

        /* 许愿树特效 */
        .tree { font-size: 8rem; margin-bottom: 20px; animation: swing 4s infinite ease-in-out; }
        @keyframes swing { 0%, 100% { transform: rotate(-2deg); } 50% { transform: rotate(2deg); } }
        .petal { position: absolute; width: 15px; height: 15px; background: #ff69b4; border-radius: 50% 0 50% 50%; pointer-events: none; opacity: 0.8; z-index: 100; }

        /* 烟花特效 */
        .firework { position: absolute; width: 6px; height: 6px; border-radius: 50%; pointer-events: none; z-index: 100; animation: explode 0.8s ease-out forwards; }
        @keyframes explode { to { transform: translate(var(--tx), var(--ty)) scale(0); opacity: 0; } }

        h1 { font-size: 2.5rem; margin-bottom: 15px; text-shadow: 2px 2px 4px rgba(0,0,0,0.3); z-index: 10; }
        p { font-size: 1.2rem; opacity: 0.9; z-index: 10; }
    </style>
</head>
<body>

    <div class="book">
        <!-- 第1页：封面 -->
        <div class="page p1 active" id="page1">
            <h1>🎂 ZD，生日快乐！</h1>
            <p>这是一份专属的电子纪念册</p>
            <div class="hint">👉 点击屏幕向右翻页</div>
        </div>

        <!-- 第2页：许愿树 -->
        <div class="page p2 hidden-right" id="page2">
            <div class="tree">🌳</div>
            <h1>诚心许愿</h1>
            <p>点击屏幕，让心愿化作花瓣飘落</p>
            <div class="hint">👉 点击屏幕向右翻页</div>
        </div>

        <!-- 第3页：烟花 -->
        <div class="page p3 hidden-right" id="page3">
            <h1>🎆 绚烂烟花</h1>
            <p>点击屏幕任意位置绽放烟花</p>
            <div class="hint">👉 点击屏幕向右翻页</div>
        </div>

        <!-- 第4页：封底 -->
        <div class="page p4 hidden-right" id="page4">
            <h1>愿你所求皆如愿 ✨</h1>
            <p>新的一岁，平安喜乐</p>
            <div class="hint" style="color:#333;">👈 点击屏幕向左翻页</div>
        </div>
    </div>

    <script>
        let currentPage = 1;
        const totalPages = 4;
        const pages = document.querySelectorAll('.page');

        // 翻页逻辑
        document.querySelector('.book').addEventListener('click', function(e) {
            // 如果是点击特效元素，不触发翻页
            if(e.target.classList.contains('petal') || e.target.classList.contains('firework')) return;

            const targetPage = e.clientX > window.innerWidth / 2 ? currentPage + 1 : currentPage - 1;
            
            if(targetPage >= 1 && targetPage <= totalPages) {
                pages[currentPage - 1].className = `page p${currentPage} hidden-${targetPage > currentPage ? 'left' : 'right'}`;
                pages[targetPage - 1].className = `page p${targetPage} active`;
                currentPage = targetPage;
            }
        });

        // 第2页：许愿树特效
        document.getElementById('page2').addEventListener('click', function(e) {
            for (let i = 0; i < 8; i++) createPetal(e.clientX, e.clientY);
        });

        function createPetal(x, y) {
            const petal = document.createElement('div');
            petal.classList.add('petal');
            document.body.appendChild(petal);
            const colors = ['#ff69b4', '#ffb6c1', '#fff0f5', '#ffd700'];
            petal.style.background = colors[Math.floor(Math.random() * colors.length)];
            const size = Math.random() * 10 + 10;
            petal.style.width = size + 'px';
            petal.style.height = size + 'px';
            petal.style.left = x + 'px';
            petal.style.top = y + 'px';
            const tx = (Math.random() - 0.5) * 200;
            const ty = Math.random() * 300 + 100;
            petal.animate([
                { transform: 'translate(0, 0) rotate(0deg)', opacity: 1 },
                { transform: `translate(${tx}px, ${ty}px) rotate(${Math.random()*360}deg)`, opacity: 0 }
            ], { duration: 2000, easing: 'ease-out' }).onfinish = () => petal.remove();
        }

        // 第3页：烟花特效
        document.getElementById('page3').addEventListener('click', function(e) {
            const colors = ['#ff6b6b','#ffd93d','#6bcb77','#4d96ff','#ff6eb4'];
            for (let i = 0; i < 15; i++) {
                const spark = document.createElement('div');
                spark.className = 'firework';
                const angle = (Math.PI * 2 / 15) * i;
                const distance = 80;
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

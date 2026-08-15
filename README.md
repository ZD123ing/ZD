<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>阻绝 生日快乐</title>
    <style>
        body {
            margin: 0;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            font-family: 'Arial', sans-serif;
            color: white;
            overflow: hidden;
            cursor: pointer; /* 提示可以点击 */
            user-select: none;
        }
        h1 {
            font-size: 4rem;
            margin: 0;
            text-shadow: 0 0 10px rgba(255,255,255,0.8);
            animation: bounce 2s infinite;
        }
        p {
            font-size: 1.5rem;
            margin-top: 20px;
            opacity: 0.9;
        }
        .hint {
            position: absolute;
            bottom: 30px;
            font-size: 1rem;
            opacity: 0.6;
            animation: pulse 1.5s infinite;
        }
        
        /* 简单的动画 */
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        @keyframes pulse {
            0%, 100% { opacity: 0.4; }
            50% { opacity: 1; }
        }

        /* 烟花粒子样式 */
        .particle {
            position: absolute;
            border-radius: 50%;
            pointer-events: none;
        }
    </style>
</head>
<body>

    <!-- 认识你这么久，很庆幸我的青春里有你。祝你生日快乐，愿你永远做自己喜欢的事，爱自己想爱的人 -->
    <h1>阻绝 生日快乐 🎂</h1>
    <p>愿你每一天都充满阳光和欢笑</p>
    


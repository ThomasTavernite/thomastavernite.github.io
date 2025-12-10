<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>tommy</title>
    <style>
        * {
            margin: 0;
            padding: 0; 
            box-sizing: border-box;
            cursor: crosshair;
        }

        ::selection {
            background: #fff;
            color: #000;
        }

        body {
            font-family: 'Courier New', monospace;
            background: #000;
            color: #fff;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }

        /* Snow effect */
        .snow {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .snowflake {
            position: absolute;
            top: -10px;
            color: #fff;
            font-size: 10px;
            animation: fall linear infinite;
        }

        @keyframes fall {
            from {
                transform: translateY(-100vh) translateX(0);
            }
            to {
                transform: translateY(100vh) translateX(50px);
            }
        }

        /* Noise texture overlay */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.03;
            z-index: 1;
            pointer-events: none;
            background-image: 
                repeating-linear-gradient(45deg, transparent, transparent 2px, rgba(255,255,255,.1) 2px, rgba(255,255,255,.1) 4px),
                repeating-linear-gradient(-45deg, transparent, transparent 2px, rgba(255,255,255,.05) 2px, rgba(255,255,255,.05) 4px);
        }

        /* Glitch effect */
        @keyframes glitch {
            0%, 100% { transform: translate(0); }
            20% { transform: translate(-1px, 1px); }
            40% { transform: translate(-1px, -1px); }
            60% { transform: translate(1px, 1px); }
            80% { transform: translate(1px, -1px); }
        }

        @keyframes flicker {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.98; }
        }

        .container {
            text-align: center;
            z-index: 2;
            position: relative;
            padding: 40px;
            animation: flicker 4s infinite;
        }

        .main-title {
            font-size: 5rem;
            font-weight: normal;
            letter-spacing: -5px;
            margin-bottom: 20px;
            position: relative;
            display: inline-block;
        }

        .main-title::before,
        .main-title::after {
            content: 'tommy';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }

        .main-title::before {
            color: #ff0000;
            animation: glitch 2s infinite;
            clip: rect(44px, 450px, 56px, 0);
            opacity: 0.8;
        }

        .main-title::after {
            color: #00ffff;
            animation: glitch 2s infinite reverse;
            clip: rect(20px, 450px, 80px, 0);
            opacity: 0.8;
        }

        .role {
            font-size: 0.9rem;
            letter-spacing: 4px;
            text-transform: uppercase;
            margin-bottom: 40px;
            opacity: 0.7;
            font-family: 'Courier New', monospace;
        }

        .links {
            display: flex;
            gap: 40px;
            justify-content: center;
            align-items: center;
            margin-top: 60px;
        }

        .link {
            color: #fff;
            text-decoration: none;
            font-size: 0.8rem;
            letter-spacing: 2px;
            text-transform: lowercase;
            position: relative;
            transition: all 0.2s;
            padding: 5px 0;
        }

        .link::before {
            content: '[';
            position: absolute;
            left: -15px;
            opacity: 0;
            transition: all 0.2s;
        }

        .link::after {
            content: ']';
            position: absolute;
            right: -15px;
            opacity: 0;
            transition: all 0.2s;
        }

        .link:hover::before,
        .link:hover::after {
            opacity: 1;
        }

        .link:hover {
            color: #ff0000;
            transform: scale(1.1);
            animation: glitch 0.3s infinite;
        }

        /* Terminal cursor blink */
        .cursor {
            display: inline-block;
            width: 10px;
            height: 20px;
            background: #fff;
            margin-left: 5px;
            animation: blink 1s infinite;
        }

        @keyframes blink {
            0%, 50% { opacity: 1; }
            51%, 100% { opacity: 0; }
        }

        /* Corner timestamps */
        .timestamp {
            position: fixed;
            font-size: 0.7rem;
            font-family: 'Courier New', monospace;
            opacity: 0.3;
            letter-spacing: 1px;
            z-index: 10;
        }

        .timestamp.top-left {
            top: 20px;
            left: 20px;
        }

        /* Scanlines */
        @keyframes scanlines {
            0% { transform: translateY(0); }
            100% { transform: translateY(100vh); }
        }

        .scanlines {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
            opacity: 0.05;
            background: repeating-linear-gradient(
                0deg,
                transparent,
                transparent 2px,
                rgba(255, 255, 255, 0.03) 2px,
                rgba(255, 255, 255, 0.03) 4px
            );
            animation: scanlines 8s linear infinite;
        }

        /* Mobile responsive */
        @media (max-width: 600px) {
            .main-title {
                font-size: 3rem;
                letter-spacing: -3px;
            }
            
            .links {
                flex-direction: column;
                gap: 20px;
            }

            .timestamp {
                display: none;
            }
        }
    </style>
</head>
<body>
    <div class="snow" id="snow"></div>
    <div class="scanlines"></div>
    
    <div class="timestamp top-left">
        <span id="time"></span>
    </div>

    <div class="container">
        <h1 class="main-title">tommy</h1>
        <div class="role">Current Role: ATL @ H&R Block<span class="cursor"></span></div>
        
        <div class="links">
            <a href="https://www.instagram.com/tommy_tavernite" target="_blank" class="link">instagram</a>
            <a href="https://www.linkedin.com/in/thomas-tavernite-1aa1672b3/" target="_blank" class="link">linkedin</a>
            <a href="mailto:tommy_1600@outlook.com" class="link">email</a>
        </div>
    </div>

    <script>
        // Create snow effect
        function createSnow() {
            const snowContainer = document.getElementById('snow');
            const snowflakeSymbols = ['•', '·', '∗', '⋅'];
            
            for (let i = 0; i < 50; i++) {
                const snowflake = document.createElement('div');
                snowflake.className = 'snowflake';
                snowflake.innerHTML = snowflakeSymbols[Math.floor(Math.random() * snowflakeSymbols.length)];
                snowflake.style.left = Math.random() * 100 + '%';
                snowflake.style.animationDuration = Math.random() * 3 + 5 + 's';
                snowflake.style.opacity = Math.random() * 0.6 + 0.2;
                snowflake.style.fontSize = Math.random() * 8 + 8 + 'px';
                snowflake.style.animationDelay = Math.random() * 5 + 's';
                snowContainer.appendChild(snowflake);
            }
        }
        
        createSnow();

        // Update timestamp
        function updateTime() {
            const now = new Date();
            const timeString = now.toLocaleString('en-US', { 
                hour12: false, 
                hour: '2-digit', 
                minute: '2-digit', 
                second: '2-digit' 
            });
            const dateString = now.toLocaleDateString('en-US', { 
                year: 'numeric', 
                month: '2-digit', 
                day: '2-digit' 
            }).replace(/\//g, '.');
            document.getElementById('time').textContent = `${dateString} ${timeString}`;
        }
        
        updateTime();
        setInterval(updateTime, 1000);

        // Random glitch effect
        setInterval(() => {
            if (Math.random() > 0.95) {
                document.body.style.transform = `translate(${Math.random() * 2 - 1}px, ${Math.random() * 2 - 1}px)`;
                setTimeout(() => {
                    document.body.style.transform = 'translate(0, 0)';
                }, 50);
            }
        }, 100);

        // Console easter egg
        console.log('%c× tommy online ×', 'color: #ff0000; font-size: 20px; font-weight: bold; text-shadow: 2px 2px 0 #000;');
        console.log('%cACCESS_GRANTED', 'color: #00ff00; font-family: monospace;');
    </script>
</body>
</html>

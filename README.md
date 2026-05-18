
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>System Override</title>
    <style>
        /* Base styles for Matrix-like atmosphere */
        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            background-color: #000000;
            font-family: 'Courier New', Courier, monospace;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #00ff00;
        }

        /* Canvas stretches over the entire background */
        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
        }

        /* UI Overlay Box for UI Elements */
        .ui-container {
            position: relative;
            z-index: 2;
            text-align: center;
        }

        /* Center Trigger Button */
        #init-btn {
            background: transparent;
            color: #00ff00;
            border: 2px solid #00ff00;
            padding: 15px 40px;
            font-size: 1.2rem;
            font-family: inherit;
            font-weight: bold;
            cursor: pointer;
            border-radius: 5px;
            box-shadow: 0 0 15px rgba(0, 255, 0, 0.4);
            transition: all 0.3s ease;
        }

        #init-btn:hover {
            background-color: #00ff00;
            color: #000000;
            box-shadow: 0 0 25px rgba(0, 255, 0, 0.8);
        }

        /* Giant Countdown Typography */
        #countdown {
            font-size: 8rem;
            font-weight: bold;
            display: none;
            text-shadow: 0 0 20px rgba(0, 255, 0, 0.7);
            margin-bottom: 20px;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>

    <!-- Matrix rain canvas -->
    <canvas id="matrix"></canvas>

    <!-- Main interactive interface -->
    <div class="ui-container">
        <button id="init-btn">INITIALIZE SYSTEM BYPASS</button>
        <div id="countdown">5</div>
    </div>

    <script>
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');
        const btn = document.getElementById('init-btn');
        const countdownEl = document.getElementById('countdown');

        // Adjust canvas dimensions dynamically
        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        resizeCanvas();
        window.addEventListener('resize', resizeCanvas);

        // Mix of binary, hexadecimal, and code operators for Matrix text rain
        const matrixChars = "01011001010101000111XX_SYS_INIT_BYPASS_TRUE_void_main()_printf_0x4F_0x7A_#include_import_os_<$>";
        const charArray = matrixChars.split("");
        
        const fontSize = 16;
        let columns = canvas.width / fontSize;
        let drops = Array(Math.floor(columns)).fill(1);

        // Render loop for the Matrix stream
        function drawMatrix() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = '#00ff00';
            ctx.font = fontSize + 'px monospace';

            for (let i = 0; i < drops.length; i++) {
                const text = charArray[Math.floor(Math.random() * charArray.length)];
                ctx.fillText(text, i * fontSize, drops[i] * fontSize);

                if (drops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }
                drops[i]++;
            }
        }

        // Trigger sequencing when clicked
        btn.addEventListener('click', () => {
            // Hide the initial action button
            btn.style.display = 'none';
            
            // Activate Matrix animation loop
            setInterval(drawMatrix, 33);

            // Activate and display the 5-second countdown timer
            countdownEl.style.display = 'block';
            let timeLeft = 5;

            const timer = setInterval(() => {
                timeLeft--;
                if (timeLeft > 0) {
                    countdownEl.textContent = timeLeft;
                } else {
                    clearInterval(timer);
                    countdownEl.textContent = "ACCESSING...";
                    
                    // Web safety feature constraint note: 
                    // Browsers strictly block scripts from launching native desktop file apps (.exe or local folders) directly.
                    // This uses a local file URL scheme to safely prompt the OS to open your default system storage view.
                    window.location.href = "file:///";
                }
            }, 1000);
        });
    </script>
</body>
</html>

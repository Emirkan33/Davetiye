<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Özel Bir Davet! 🧸🌸</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Fredoka', cursive, sans-serif;
            background: linear-gradient(135deg, #ffe4e6 0%, #fbcfe8 50%, #f472b6 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Uçuşan Çiçekler ve Ayıcıklar */
        @keyframes float {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            20% { opacity: 0.8; }
            80% { opacity: 0.8; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        .floating-element {
            position: absolute;
            animation: float 8s infinite linear;
            pointer-events: none;
            z-index: 1;
        }

        /* Tatlı Buton Animasyonları */
        .btn-yes {
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .bear-bounce {
            animation: bounce 1.5s infinite alternate;
        }

        @keyframes bounce {
            0% { transform: translateY(0); }
            100% { transform: translateY(-15px); }
        }
    </style>
</head>
<body class="relative flex flex-col items-center justify-center min-h-screen p-4 select-none">

    <!-- Arka Plan Süslemeleri (Çiçekler ve Ayıcıklar) -->
    <div id="floating-container" class="absolute inset-0 overflow-hidden pointer-events-none z-0"></div>

    <!-- Soru Kartı -->
    <div id="card" class="relative z-10 bg-white/80 backdrop-blur-md p-8 sm:p-12 rounded-3xl shadow-2xl border-4 border-pink-300 text-center max-w-lg w-full flex flex-col items-center justify-center transition-all duration-300">
        
        <!-- Sevimli Görsel / GIF -->
        <div id="gif-container" class="mb-6 bear-bounce">
            <img id="main-gif" src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExM3Zudm90NDdybmsxbDF2OXE1bTNndndnMHZqazI4M2V4eW43djN2OCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/cLS1cfxvGOPVpf9g3y/giphy.gif" alt="Cute Bear" class="w-40 h-40 object-contain drop-shadow-md">
        </div>

        <h1 id="question-text" class="text-2xl sm:text-3xl font-bold text-pink-600 mb-8 leading-snug drop-shadow-sm">
            Yarın akşam benimle gezer misin? 🧸🌸
        </h1>

        <!-- Butonlar -->
        <div id="button-group" class="flex flex-wrap items-center justify-center gap-4 w-full relative min-h-[80px]">
            <button id="yes-btn" onclick="handleYesClick()" class="btn-yes bg-pink-500 hover:bg-pink-600 text-white font-bold py-3 px-8 rounded-full shadow-lg shadow-pink-500/40 transform hover:scale-110 active:scale-95 text-lg z-20">
                Evet! 🥰
            </button>
            <button id="no-btn" onclick="handleNoClick()" class="bg-gray-200 hover:bg-gray-300 text-gray-700 font-bold py-3 px-6 rounded-full shadow transition-all duration-200 text-base z-10">
                Hayır 🥺
            </button>
        </div>
    </div>

    <!-- Kabul Edilince Açılan Ekran -->
    <div id="success-screen" class="hidden relative z-30 bg-white/90 backdrop-blur-lg p-8 sm:p-12 rounded-3xl shadow-2xl border-4 border-pink-400 text-center max-w-md w-full flex flex-col items-center animate-fade-in">
        <div class="mb-6 bear-bounce">
            <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExN3Znd2N3OTdtZ24wcXBqbzU2OHljcGp2b2V3dW1sOHZrbXQ1aDFnbCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/MDJ9IbxxvDUQM/giphy.gif" alt="Happy Bear" class="w-48 h-48 object-contain drop-shadow-lg">
        </div>
        <h2 class="text-3xl font-extrabold text-pink-600 mb-3">Harikasın! 🎉💖</h2>
        <p class="text-xl font-semibold text-gray-700 leading-relaxed">
            Yarın akşam seni 7'de alırım! 🌸🧸✨
        </p>
    </div>

    <script>
        let noCount = 0;
        const yesBtn = document.getElementById('yes-btn');
        const noBtn = document.getElementById('no-btn');
        const questionText = document.getElementById('question-text');
        const mainGif = document.getElementById('main-gif');

        // Hayır butonuna basıldığında değişecek tatlı mesajlar
        const noMessages = [
            "Emin misin? 🥺",
            "Bir daha düşün bence! 🌸",
            "Gerçekten hayır mı? 🐻",
            "Bak üzülürüm ama... 💔",
            "Lütfen evet de! 💕",
            "Son kararın mı? 🙈",
            "Kaçışın yok, evet diyeceksin! 😄"
        ];

        // Hayır butonuna basılınca değişecek tatlı ayıcık görselleri
        const bearGifs = [
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNm4zaHowZnEycTZ0ZWJ4MGY2azA4bWkyaTFkcmkzaW10NjYzbXlybiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/9Y1LEFK34BzA4/giphy.gif",
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMnllOHZtbmtxMGpjaHowMjl6bXkyenRnd3F2d2lsZHN6bzNzZXljNSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/13CoXDiaCcCoyk/giphy.gif",
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNWYwZXRjNXhxcWhhbHFiaDF1YWN3dm1uYngyYnZzcXpya3J4MmNtNSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9cw/d2lcHJTG5TpwPM4w/giphy.gif"
        ];

        function handleNoClick() {
            noCount++;
            
            // Mesajı ve görseli değiştir
            const msgIndex = Math.min(noCount - 1, noMessages.length - 1);
            noBtn.innerText = noMessages[msgIndex];
            
            const gifIndex = Math.min(noCount - 1, bearGifs.length - 1);
            mainGif.src = bearGifs[gifIndex];

            // Evet butonunu aşamalı olarak büyüt
            if (noCount <= 6) {
                const newSize = 1 + (noCount * 0.45); // Buton her seferinde %45 büyür
                const newPaddingY = 12 + (noCount * 10);
                const newPaddingX = 32 + (noCount * 20);
                const newFontSize = 18 + (noCount * 6);

                yesBtn.style.transform = `scale(${newSize})`;
                yesBtn.style.padding = `${newPaddingY}px ${newPaddingX}px`;
                yesBtn.style.fontSize = `${newFontSize}px`;
            } else {
                // En sonunda Evet butonu tüm ekranı kaplasın!
                yesBtn.style.position = 'fixed';
                yesBtn.style.top = '0';
                yesBtn.style.left = '0';
                yesBtn.style.width = '100vw';
                yesBtn.style.height = '100vh';
                yesBtn.style.zIndex = '9999';
                yesBtn.style.borderRadius = '0';
                yesBtn.style.fontSize = '3rem';
                yesBtn.innerText = 'EVET! (BAŞKA ÇAREN YOK 💖)';
                noBtn.style.display = 'none';
            }
        }

        function handleYesClick() {
            // Soru kartını gizle, başarı ekranını göster
            document.getElementById('card').classList.add('hidden');
            document.getElementById('success-screen').classList.remove('hidden');

            // Renkli konfeti patlaması
            const duration = 3 * 1000;
            const end = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 7,
                    angle: 60,
                    spread: 55,
                    origin: { x: 0, y: 0.7 },
                    colors: ['#ec4899', '#f43f5e', '#fb7185', '#ffffff']
                });
                confetti({
                    particleCount: 7,
                    angle: 120,
                    spread: 55,
                    origin: { x: 1, y: 0.7 },
                    colors: ['#ec4899', '#f43f5e', '#fb7185', '#ffffff']
                });

                if (Date.now() < end) {
                    requestAnimationFrame(frame);
                }
            }());
        }

        // Arka planda uçuşan ayıcık ve çiçek simgeleri oluşturma
        function createFloatingElements() {
            const container = document.getElementById('floating-container');
            const items = ['🌸', '🧸', '🌺', '🌷', '💖', '💐', '🐻'];

            setInterval(() => {
                if (container.childElementCount > 30) return;

                const element = document.createElement('div');
                element.className = 'floating-element';
                element.innerText = items[Math.floor(Math.random() * items.length)];

                const size = Math.random() * 20 + 20; // 20px - 40px
                const leftPos = Math.random() * 100;
                const animDuration = Math.random() * 5 + 5; // 5s - 10s

                element.style.fontSize = `${size}px`;
                element.style.left = `${leftPos}%`;
                element.style.animationDuration = `${animDuration}s`;

                container.appendChild(element);

                setTimeout(() => {
                    element.remove();
                }, animDuration * 1000);
            }, 300);
        }

        window.onload = createFloatingElements;
    </script>
</body>
</html>

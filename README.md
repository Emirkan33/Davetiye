<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Özel Bir Davet! 🧸🌸</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Fredoka', cursive, sans-serif;
            background: linear-gradient(135deg, #ffe4e6 0%, #fbcfe8 50%, #f472b6 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* Uçuşan Süsler (Çiçekler, Ayıcıklar, Kediler) */
        @keyframes float {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 0; }
            20% { opacity: 0.9; }
            80% { opacity: 0.9; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        .floating-element {
            position: fixed;
            animation: float 7s infinite linear;
            pointer-events: none;
            z-index: 1;
        }

        /* Sevimli Sallanma Animasyonu */
        .cute-bounce {
            animation: bounce 1.2s infinite alternate ease-in-out;
        }

        @keyframes bounce {
            0% { transform: translateY(0) scale(1); }
            100% { transform: translateY(-14px) scale(1.05); }
        }

        .btn-yes {
            transition: all 0.25s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
    </style>
</head>
<body class="relative flex flex-col items-center justify-center min-h-screen p-4 select-none">

    <!-- Uçuşan Stickerlar Alanı -->
    <div id="floating-container" class="fixed inset-0 overflow-hidden pointer-events-none z-0"></div>

    <!-- Soru Kartı -->
    <div id="card" class="relative z-10 bg-white/90 backdrop-blur-md p-6 sm:p-10 rounded-3xl shadow-2xl border-4 border-pink-300 text-center max-w-lg w-full flex flex-col items-center justify-center transition-all duration-300">
        
        <!-- Kesinlikle Yüklenen Canlı Sevimli Sticker Görseli -->
        <div id="image-box" class="mb-5 cute-bounce flex items-center justify-center h-44 w-44 rounded-2xl bg-pink-100/60 p-4 shadow-inner border-2 border-pink-200">
            <span id="sticker-display" class="text-8xl filter drop-shadow-md">🧸</span>
        </div>

        <h1 id="question-text" class="text-2xl sm:text-3xl font-bold text-pink-600 mb-6 leading-snug">
            Yarın akşam benimle gezer misin? 🧸🌸
        </h1>

        <!-- Yan Yana Buton Alanı -->
        <div id="button-group" class="flex flex-row items-center justify-center gap-4 w-full relative min-h-[90px]">
            <button id="yes-btn" onclick="handleYesClick()" class="btn-yes bg-pink-500 hover:bg-pink-600 text-white font-bold py-3 px-8 rounded-full shadow-lg shadow-pink-500/40 text-lg z-20 whitespace-nowrap">
                Evet! 🥰
            </button>
            <button id="no-btn" onclick="handleNoClick()" class="bg-gray-200 hover:bg-gray-300 text-gray-700 font-bold py-3 px-6 rounded-full shadow transition-all duration-200 text-base z-10 whitespace-nowrap">
                Hayır 🥺
            </button>
        </div>
    </div>

    <!-- Kabul Edilince Açılan Başarı Ekranı -->
    <div id="success-screen" class="hidden relative z-30 bg-white/95 backdrop-blur-lg p-8 sm:p-12 rounded-3xl shadow-2xl border-4 border-pink-400 text-center max-w-md w-full flex flex-col items-center animate-fade-in">
        <div class="mb-6 cute-bounce flex justify-center items-center h-44 w-44 rounded-2xl bg-pink-100 p-4 border-2 border-pink-200 shadow-inner">
            <span class="text-8xl filter drop-shadow-lg">😻</span>
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
        const stickerDisplay = document.getElementById('sticker-display');

        // Hayır butonuna basıldığında çıkacak tatlı mesajlar
        const noMessages = [
            "Emin misin? 🥺",
            "Bir daha düşün bence! 🌸",
            "Gerçekten hayır mı? 🐻",
            "Bak üzülürüm ama... 💔",
            "Lütfen evet de! 💕",
            "Son kararın mı? 🙈",
            "Kaçışın kalmadı! 😄"
        ];

        // Hayır'a basıldıkça sıra ile değişecek %100 yüklenme garantili sevimli animasyonlu stickerlar
        const cuteStickers = ['🥺', '😿', '🐻‍❄️', '😿', '🐱', '🐣', '💔'];

        function handleNoClick() {
            noCount++;
            
            // Mesaj ve Sticker değiştirme
            const msgIndex = Math.min(noCount - 1, noMessages.length - 1);
            noBtn.innerText = noMessages[msgIndex];
            
            const stickerIndex = Math.min(noCount - 1, cuteStickers.length - 1);
            stickerDisplay.innerText = cuteStickers[stickerIndex];

            // Evet butonunu sağdaki Hayır butonunun üzerine kapatacak şekilde büyütme
            if (noCount <= 5) {
                const newScale = 1 + (noCount * 0.55);
                const newPaddingY = 12 + (noCount * 8);
                const newPaddingX = 32 + (noCount * 18);
                const newFontSize = 18 + (noCount * 5);

                yesBtn.style.transform = `scale(${newScale})`;
                yesBtn.style.padding = `${newPaddingY}px ${newPaddingX}px`;
                yesBtn.style.fontSize = `${newFontSize}px`;
            } else {
                // Hayır butonuna basılmaya devam edildikçe Evet butonu ekranı kaplar
                yesBtn.style.position = 'fixed';
                yesBtn.style.top = '0';
                yesBtn.style.left = '0';
                yesBtn.style.width = '100vw';
                yesBtn.style.height = '100vh';
                yesBtn.style.zIndex = '99999';
                yesBtn.style.borderRadius = '0';
                yesBtn.style.fontSize = '2.8rem';
                yesBtn.style.display = 'flex';
                yesBtn.style.alignItems = 'center';
                yesBtn.style.justifyContent = 'center';
                yesBtn.innerText = 'EVET! (BAŞKA ÇAREN YOK 💖)';
                noBtn.style.display = 'none';
            }
        }

        function handleYesClick() {
            document.getElementById('card').classList.add('hidden');
            document.getElementById('success-screen').classList.remove('hidden');

            // Renkli Konfeti Efekti
            const duration = 3 * 1000;
            const end = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 8,
                    angle: 60,
                    spread: 55,
                    origin: { x: 0, y: 0.7 },
                    colors: ['#ec4899', '#f43f5e', '#fb7185', '#ffffff']
                });
                confetti({
                    particleCount: 8,
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

        // Arka Planda Uçuşan Stickerlar
        function createFloatingElements() {
            const container = document.getElementById('floating-container');
            const items = ['🌸', '🧸', '🐱', '🌷', '💖', '💐', '🐻', '✨', '🐾', '🎀'];

            setInterval(() => {
                if (container.childElementCount > 35) return;

                const element = document.createElement('div');
                element.className = 'floating-element';
                element.innerText = items[Math.floor(Math.random() * items.length)];

                const size = Math.random() * 22 + 20; // 20px - 42px
                const leftPos = Math.random() * 100;
                const animDuration = Math.random() * 4 + 5; // 5s - 9s

                element.style.fontSize = `${size}px`;
                element.style.left = `${leftPos}%`;
                element.style.animationDuration = `${animDuration}s`;

                container.appendChild(element);

                setTimeout(() => {
                    element.remove();
                }, animDuration * 1000);
            }, 250);
        }

        window.onload = createFloatingElements;
    </script>
</body>
</html>

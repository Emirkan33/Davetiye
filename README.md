<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Özel Bir Davet! 🧸🌸</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- EmailJS Kütüphanesi -->
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
    <script type="text/javascript">
        (function() {
            emailjs.init("P6my-X1rwuebozDZo"); // Public Key
        })();
    </script>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }

        body {
            font-family: 'Fredoka', cursive, sans-serif;
            background: linear-gradient(135deg, #f43f5e 0%, #ec4899 50%, #f472b6 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }

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

        .option-card {
            transition: all 0.2s ease-in-out;
            cursor: pointer;
        }

        .option-card:hover {
            transform: translateY(-5px);
            border-color: #f43f5e;
            background-color: #fff1f2;
        }

        .option-card.selected {
            border-color: #f43f5e;
            background-color: #ffe4e6;
            box-shadow: 0 10px 15px -3px rgba(244, 63, 94, 0.3);
        }
    </style>
</head>
<body class="relative flex flex-col items-center justify-center min-h-screen p-4 select-none">

    <!-- Uçuşan Stickerlar Alanı -->
    <div id="floating-container" class="fixed inset-0 overflow-hidden pointer-events-none z-0"></div>

    <!-- 1. Aşama: Soru Kartı -->
    <div id="card" class="relative z-10 bg-white/95 backdrop-blur-md p-6 sm:p-10 rounded-3xl shadow-2xl border-4 border-pink-400 text-center max-w-lg w-full flex flex-col items-center justify-center transition-all duration-300">
        <div id="image-box" class="mb-5 cute-bounce flex items-center justify-center h-44 w-44 rounded-2xl bg-pink-100/80 p-4 shadow-inner border-2 border-pink-200">
            <span id="sticker-display" class="text-8xl filter drop-shadow-md">🧸</span>
        </div>

        <h1 id="question-text" class="text-2xl sm:text-3xl font-bold text-pink-600 mb-6 leading-snug">
            Selam Prenses, bu güzel davetiye sadece sana layık! 🧸🌸
        </h1>

        <div id="button-group" class="flex flex-row items-center justify-center gap-4 w-full relative min-h-[90px]">
            <button id="yes-btn" onclick="handleFirstYesClick()" class="btn-yes bg-pink-600 hover:bg-pink-700 text-white font-bold py-3 px-8 rounded-full shadow-lg shadow-pink-500/40 text-lg z-20 whitespace-nowrap">
                Evet! 🥰
            </button>
            <button id="no-btn" onclick="handleNoClick()" class="bg-gray-200 hover:bg-gray-300 text-gray-700 font-bold py-3 px-6 rounded-full shadow transition-all duration-200 text-base z-10 whitespace-nowrap">
                Hayır 🥺
            </button>
        </div>
    </div>

    <!-- 2. Aşama: Tarih ve Saat Seçim Ekranı -->
    <div id="date-screen" class="hidden relative z-30 bg-white/95 backdrop-blur-lg p-8 sm:p-12 rounded-3xl shadow-2xl border-4 border-pink-400 text-center max-w-md w-full flex flex-col items-center">
        <div class="mb-4 cute-bounce flex justify-center items-center h-32 w-32 rounded-2xl bg-pink-100 p-4 border-2 border-pink-200 shadow-inner">
            <span class="text-6xl filter drop-shadow-lg">💐✨</span>
        </div>
        <h2 class="text-2xl sm:text-3xl font-extrabold text-pink-600 mb-2">Teşekkürler Prenses! 🌸</h2>
        <p class="text-gray-600 mb-6 font-medium">Buluşmamız için ne zaman görüşelim?</p>
        
        <div class="flex flex-col gap-4 w-full mb-6">
            <div>
                <label class="block text-sm font-semibold text-gray-700 mb-1 text-left">Tarih Seç:</label>
                <input type="date" id="date-input" class="w-full p-3 border-2 border-pink-300 rounded-2xl focus:outline-none focus:border-pink-500 text-gray-700 font-medium bg-pink-50/50">
            </div>
            <div>
                <label class="block text-sm font-semibold text-gray-700 mb-1 text-left">Saat Seç:</label>
                <input type="time" id="time-input" value="19:00" class="w-full p-3 border-2 border-pink-300 rounded-2xl focus:outline-none focus:border-pink-500 text-gray-700 font-medium bg-pink-50/50">
            </div>
        </div>

        <button onclick="handleDateSubmit()" class="w-full bg-pink-600 hover:bg-pink-700 text-white font-bold py-3 px-6 rounded-full shadow-lg shadow-pink-500/40 text-lg transition-all">
            Onayla ve Devam Et 💕
        </button>
    </div>

    <!-- 3. Aşama: Etkinlik Seçim Tablosu -->
    <div id="activity-screen" class="hidden relative z-30 bg-white/95 backdrop-blur-lg p-6 sm:p-8 rounded-3xl shadow-2xl border-4 border-pink-400 text-center max-w-lg w-full flex flex-col items-center">
        <h2 class="text-2xl font-extrabold text-pink-600 mb-2">Ne yapmak istersin? 🎀</h2>
        <p class="text-gray-600 mb-6 text-sm font-medium">Aşağıdan favori aktiviteni seçebilirsin:</p>

        <div class="grid grid-cols-2 gap-4 w-full mb-6">
            <div onclick="selectActivity(this, 'Yemek 🍝')" class="option-card flex flex-col items-center p-4 border-2 border-pink-200 rounded-2xl bg-pink-50/30">
                <span class="text-4xl mb-2">🍝</span>
                <span class="font-bold text-gray-700">Yemek</span>
            </div>
            <div onclick="selectActivity(this, 'Film 🎬')" class="option-card flex flex-col items-center p-4 border-2 border-pink-200 rounded-2xl bg-pink-50/30">
                <span class="text-4xl mb-2">🎬</span>
                <span class="font-bold text-gray-700">Film</span>
            </div>
            <div onclick="selectActivity(this, 'Yürüyüş 🚶‍♀️')" class="option-card flex flex-col items-center p-4 border-2 border-pink-200 rounded-2xl bg-pink-50/30">
                <span class="text-4xl mb-2">🚶‍♀️</span>
                <span class="font-bold text-gray-700">Yürüyüş</span>
            </div>
            <div onclick="selectActivity(this, 'Oyun 🎮')" class="option-card flex flex-col items-center p-4 border-2 border-pink-200 rounded-2xl bg-pink-50/30">
                <span class="text-4xl mb-2">🎮</span>
                <span class="font-bold text-gray-700">Oyun</span>
            </div>
            <div onclick="selectActivity(this, 'Karışık 🎁')" class="option-card flex flex-col items-center p-4 border-2 border-pink-200 rounded-2xl bg-pink-50/30">
                <span class="text-4xl mb-2">🎁</span>
                <span class="font-bold text-gray-700">Karışık</span>
            </div>
            <div onclick="selectActivity(this, 'Beyime bırakıyorum ✨')" class="option-card flex flex-col items-center p-4 border-2 border-pink-200 rounded-2xl bg-pink-50/30">
                <span class="text-4xl mb-2">✨</span>
                <span class="font-bold text-gray-700 text-xs sm:text-sm">Beyime bırakıyorum</span>
            </div>
        </div>

        <button onclick="handleActivitySubmit()" class="w-full bg-pink-600 hover:bg-pink-700 text-white font-bold py-3 px-6 rounded-full shadow-lg shadow-pink-500/40 text-lg transition-all">
            Seçimi Tamamla 💖
        </button>
    </div>

    <!-- 4. Aşama: Final Başarı Ekranı -->
    <div id="success-screen" class="hidden relative z-30 bg-white/95 backdrop-blur-lg p-8 sm:p-12 rounded-3xl shadow-2xl border-4 border-pink-400 text-center max-w-md w-full flex flex-col items-center animate-fade-in">
        <div class="mb-6 cute-bounce flex justify-center items-center h-44 w-44 rounded-2xl bg-pink-100 p-4 border-2 border-pink-200 shadow-inner">
            <span class="text-8xl filter drop-shadow-lg">😻</span>
        </div>
        <h2 class="text-3xl font-extrabold text-pink-600 mb-3">Harikasın! 🎉💖</h2>
        <p id="final-details" class="text-lg font-semibold text-gray-700 leading-relaxed">
            Randevumuz onaylandı, sabırsızlıkla bekliyorum! 🌸🧸✨
        </p>
    </div>

    <script>
        let noCount = 0;
        let selectedDate = '';
        let selectedTime = '';
        let selectedActivityType = '';
        
        const yesBtn = document.getElementById('yes-btn');
        const noBtn = document.getElementById('no-btn');
        const stickerDisplay = document.getElementById('sticker-display');

        const noMessages = [
            "Emin misin? 🥺",
            "Bir daha düşün bence! 🌸",
            "Gerçekten hayır mı? 🐻",
            "Bak üzülürüm ama... 💔",
            "Lütfen evet de! 💕",
            "Son kararın mı? 🙈",
            "Kaçışın kalmadı! 😄"
        ];

        const cuteStickers = ['🥺', '😿', '🐻‍❄️', '😿', '🐱', '🐣', '💔'];

        function handleNoClick() {
            noCount++;
            const msgIndex = Math.min(noCount - 1, noMessages.length - 1);
            noBtn.innerText = noMessages[msgIndex];
            
            const stickerIndex = Math.min(noCount - 1, cuteStickers.length - 1);
            stickerDisplay.innerText = cuteStickers[stickerIndex];

            if (noCount <= 5) {
                const newScale = 1 + (noCount * 0.55);
                const newPaddingY = 12 + (noCount * 8);
                const newPaddingX = 32 + (noCount * 18);
                const newFontSize = 18 + (noCount * 5);

                yesBtn.style.transform = `scale(${newScale})`;
                yesBtn.style.padding = `${newPaddingY}px ${newPaddingX}px`;
                yesBtn.style.fontSize = `${newFontSize}px`;
            } else {
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

        function handleFirstYesClick() {
            document.getElementById('card').classList.add('hidden');
            document.getElementById('date-screen').classList.remove('hidden');
        }

        function handleDateSubmit() {
            selectedDate = document.getElementById('date-input').value;
            selectedTime = document.getElementById('time-input').value;

            if(!selectedDate) {
                alert('Lütfen bir tarih seçebilir misin prenses? 🌸');
                return;
            }
            document.getElementById('date-screen').classList.add('hidden');
            document.getElementById('activity-screen').classList.remove('hidden');
        }

        function selectActivity(element, type) {
            document.querySelectorAll('.option-card').forEach(card => card.classList.remove('selected'));
            element.classList.add('selected');
            selectedActivityType = type;
        }

        function handleActivitySubmit() {
            if(!selectedActivityType) {
                alert('Lütfen bir aktivite seçmeyi unutma! 🧸');
                return;
            }

            document.getElementById('activity-screen').classList.add('hidden');
            document.getElementById('success-screen').classList.remove('hidden');

            // EmailJS ile mail gönderme işlemi
            const templateParams = {
                date: selectedDate,
                time: selectedTime,
                activity: selectedActivityType
            };

            emailjs.send('service_1fnwyzh', 'template_bocuyax', templateParams)
                .then(function(response) {
                    console.log('SUCCESS!', response.status, response.text);
                }, function(error) {
                    console.log('FAILED...', error);
                });

            // Romantik kırmızı/pembe konfeti şöleni
            const duration = 4 * 1000;
            const end = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 10,
                    angle: 60,
                    spread: 60,
                    origin: { x: 0, y: 0.7 },
                    colors: ['#dc2626', '#e11d48', '#f43f5e', '#fb7185', '#ffffff']
                });
                confetti({
                    particleCount: 10,
                    angle: 120,
                    spread: 60,
                    origin: { x: 1, y: 0.7 },
                    colors: ['#dc2626', '#e11d48', '#f43f5e', '#fb7185', '#ffffff']
                });

                if (Date.now() < end) {
                    requestAnimationFrame(frame);
                }
            }());
        }

        function createFloatingElements() {
            const container = document.getElementById('floating-container');
            const items = ['🌸', '🧸', '💖', '🌷', '💐', '🐻', '✨', '🌹', '❤️'];

            setInterval(() => {
                if (container.childElementCount > 35) return;

                const element = document.createElement('div');
                element.className = 'floating-element';
                element.innerText = items[Math.floor(Math.random() * items.length)];

                const size = Math.random() * 22 + 20;
                const leftPos = Math.random() * 100;
                const animDuration = Math.random() * 4 + 5;

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

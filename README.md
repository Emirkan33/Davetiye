<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>I Love You in 20 Languages 💖</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background: radial-gradient(circle at center, #1a0b1c 0%, #0d0410 100%);
            color: #f3f4f6;
            overflow-x: hidden;
            min-height: 100vh;
        }

        .glass-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
            transition: all 0.3s ease;
        }

        .glass-card:hover {
            background: rgba(255, 255, 255, 0.12);
            border-color: rgba(244, 63, 94, 0.6);
            box-shadow: 0 12px 40px 0 rgba(244, 63, 94, 0.3);
            transform: scale(1.08);
            z-index: 50;
        }

        @keyframes pulse-glow {
            0%, 100% { text-shadow: 0 0 10px rgba(244, 63, 94, 0.6), 0 0 20px rgba(244, 63, 94, 0.4); }
            50% { text-shadow: 0 0 20px rgba(244, 63, 94, 0.9), 0 0 30px rgba(236, 72, 153, 0.8); }
        }

        .neon-title {
            animation: pulse-glow 3s infinite ease-in-out;
        }

        @keyframes floatUp {
            0% { transform: translateY(100vh) scale(0.5); opacity: 0; }
            20% { opacity: 0.8; }
            80% { opacity: 0.8; }
            100% { transform: translateY(-10vh) scale(1.2); opacity: 0; }
        }

        .floating-heart {
            position: absolute;
            color: rgba(244, 63, 94, 0.6);
            animation: floatUp 6s infinite linear;
            bottom: -20px;
            pointer-events: none;
            z-index: 1;
        }

        /* Kalp Formasyonu için Özel Konumlandırma Matrisi */
        .heart-grid {
            display: grid;
            grid-template-columns: repeat(7, minmax(0, 1fr));
            gap: 12px;
            max-width: 850px;
            margin: 0 auto;
        }

        /* Kalp şeklini vermek için bazı hücreleri boş bırakıyor veya hizalıyoruz */
        .heart-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 10px;
            border-radius: 1rem;
            cursor: pointer;
            text-align: center;
            min-height: 90px;
        }

        /* Mobil uyum için */
        @media (max-width: 768px) {
            .heart-grid {
                grid-template-columns: repeat(3, minmax(0, 1fr));
            }
        }
    </style>
</head>
<body class="relative flex flex-col min-h-screen selection:bg-rose-500 selection:text-white">

    <div id="hearts-container" class="absolute inset-0 overflow-hidden pointer-events-none z-0"></div>

    <header class="relative z-10 w-full max-w-6xl mx-auto px-4 py-6 flex flex-col sm:flex-row justify-between items-center gap-4">
        <div class="flex items-center gap-3">
            <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-rose-600 to-pink-500 flex items-center justify-center shadow-lg shadow-rose-500/30">
                <i class="fa-solid fa-heart text-white text-xl animate-pulse"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold bg-gradient-to-r from-rose-400 via-pink-300 to-purple-400 bg-clip-text text-transparent">Kalpten Kalbe</h1>
                <p class="text-xs text-rose-300/70">20 Dilde Seni Seviyorum</p>
            </div>
        </div>
        <div class="flex items-center gap-3">
            <button onclick="triggerGlobalCelebration()" class="px-4 py-2.5 rounded-xl bg-gradient-to-r from-rose-600 to-pink-600 hover:from-rose-500 hover:to-pink-500 text-white font-medium text-sm shadow-lg shadow-rose-600/30 transition-all duration-300 transform hover:scale-105 active:scale-95 flex items-center gap-2">
                <i class="fa-solid fa-wand-magic-sparkles"></i> Kutlama Modu
            </button>
            <button onclick="togglePythonModal(true)" class="px-4 py-2.5 rounded-xl glass-card hover:bg-white/10 text-rose-200 font-medium text-sm transition-all duration-300 transform hover:scale-105 active:scale-95 flex items-center gap-2 border border-rose-500/30">
                <i class="fa-brands fa-python text-rose-400"></i> Python Kod
            </button>
        </div>
    </header>

    <main class="relative z-10 w-full max-w-5xl mx-auto px-4 flex-grow flex flex-col items-center justify-center my-6">
        <div class="text-center max-w-2xl mb-8">
            <h2 class="text-3xl sm:text-4xl font-extrabold text-white mb-3 tracking-tight neon-title">
                💖 Kalbimin İçinden 💖
            </h2>
            <p class="text-sm sm:text-base text-gray-300/90 leading-relaxed">
                Dünyanın dört bir yanından aşk sözleri kalp formunda bir araya geldi. Kartlara tıklayarak sesli dinleyebilir ve kutlama patlaması yaratabilirsin!
            </p>
        </div>

        <!-- Kalp Şeklindeki Grid Alanı -->
        <div id="heart-container-grid" class="grid grid-cols-2 sm:grid-cols-4 md:grid-cols-5 gap-4 w-full">
            <!-- JavaScript ile dinamik dolacak -->
        </div>
    </main>

    <footer class="relative z-10 w-full text-center py-6 text-xs text-gray-400 border-t border-white/5 mt-auto">
        <p>Sonsuz sevgi ve modern web teknolojileriyle hazırlandı ❤️</p>
    </footer>

    <!-- Python Modal -->
    <div id="python-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden transition-opacity duration-300 opacity-0">
        <div class="glass-card w-full max-w-3xl rounded-3xl p-6 border border-rose-500/30 shadow-2xl relative max-h-[90vh] flex flex-col">
            <div class="flex justify-between items-center pb-4 border-b border-white/10">
                <div class="flex items-center gap-3">
                    <div class="w-8 h-8 rounded-lg bg-blue-500/20 text-blue-400 flex items-center justify-center">
                        <i class="fa-brands fa-python text-lg"></i>
                    </div>
                    <h3 class="text-lg font-bold text-white">Python Kaynak Kodu</h3>
                </div>
                <button onclick="togglePythonModal(false)" class="w-8 h-8 rounded-full bg-white/5 hover:bg-white/10 flex items-center justify-center text-gray-400 hover:text-white transition-colors">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <div class="py-4 overflow-y-auto flex-grow font-mono text-xs sm:text-sm text-rose-100/90 bg-[#09020c]/80 p-4 rounded-xl border border-white/5">
                <pre><code id="python-code-content"></code></pre>
            </div>
            <div class="pt-4 flex justify-between items-center border-t border-white/10">
                <span class="text-xs text-gray-400">Python 3.10+ Uyumlu Kalp Matrisi</span>
                <button onclick="copyPythonCode()" class="px-4 py-2 rounded-xl bg-rose-600/80 hover:bg-rose-600 text-white text-xs font-semibold transition-all flex items-center gap-2">
                    <i class="fa-regular fa-copy"></i> Kodu Kopyala
                </button>
            </div>
        </div>
    </div>

    <script>
        const languagesData = [
            { id: 1, lang: "İngilizce", flag: "🇺🇸", phrase: "I love you", phonetic: "Eye luv yoo" },
            { id: 2, lang: "Türkçe", flag: "🇹🇷", phrase: "Seni seviyorum", phonetic: "Seh-nee seh-vee-yo-rum" },
            { id: 3, lang: "Fransızca", flag: "🇫🇷", phrase: "Je t'aime", phonetic: "Zhuh tem" },
            { id: 4, lang: "İspanyolca", flag: "🇪🇸", phrase: "Te amo", phonetic: "Teh ah-mo" },
            { id: 5, lang: "Almanca", flag: "🇩🇪", phrase: "Ich liebe dich", phonetic: "Ish lee-buh dish" },
            { id: 6, lang: "İtalyanca", flag: "🇮🇹", phrase: "Ti amo", phonetic: "Tee ah-mo" },
            { id: 7, lang: "Japonca", flag: "🇯🇵", phrase: "愛してる", phonetic: "Ai-shi-te-ru" },
            { id: 8, lang: "Korece", flag: "🇰🇷", phrase: "사랑해", phonetic: "Sah-rang-hae" },
            { id: 9, lang: "Çince", flag: "🇨🇳", phrase: "我爱你", phonetic: "Woh eye nee" },
            { id: 10, lang: "Portekizce", flag: "🇧🇷", phrase: "Eu amo-te", phonetic: "Eh-oo ah-mo-teh" },
            { id: 11, lang: "Rusça", flag: "🇷🇺", phrase: "Я тебя люблю", phonetic: "Ya tyeb-ya lyub-lyu" },
            { id: 12, lang: "Yunanca", flag: "🇬🇷", phrase: "Σ' αγαπώ", phonetic: "Sah-gah-poh" },
            { id: 13, lang: "Arapça", flag: "🇸🇦", phrase: "أحبك", phonetic: "Oo-hib-bu-ka" },
            { id: 14, lang: "Hintçe", flag: "🇮🇳", phrase: "मैं तुमसे प्यार करता हूँ", phonetic: "Main tumse pyaar" },
            { id: 15, lang: "Flemenkçe", flag: "🇳🇱", phrase: "Ik hou van jou", phonetic: "Ik how vahn yow" },
            { id: 16, lang: "İsveççe", flag: "🇸🇪", phrase: "Jag älskar dig", phonetic: "Yahg el-skar day" },
            { id: 17, lang: "Lehçe", flag: "🇵🇱", phrase: "Kocham Cię", phonetic: "Ko-ham chye" },
            { id: 18, lang: "Tagalog", flag: "🇵🇭", phrase: "Mahal kita", phonetic: "Ma-hal kee-ta" },
            { id: 19, lang: "Vietnamca", flag: "🇻🇳", phrase: "Anh yêu em", phonetic: "Anh yew em" },
            { id: 20, lang: "İrlanda G.', flag: "🇮🇪", phrase: "Tá grá agam ort", phonetic: "Taw graw ah-gum" }
        ];

        const pythonCodeString = `# -*- coding: utf-8 -*-
# 20 Dilde Kalp Formatında Seni Seviyorum

love_languages = [
    ("🇺🇸", "English", "I love you"),
    ("🇹🇷", "Turkish", "Seni seviyorum"),
    ("🇫🇷", "French", "Je t'aime"),
    ("🇪🇸", "Spanish", "Te amo"),
    ("🇩🇪", "German", "Ich liebe dich"),
    ("🇮🇹", "Italian", "Ti amo"),
    ("🇯🇵", "Japanese", "愛してる"),
    ("🇰🇷", "Korean", "사랑해"),
    ("🇨🇳", "Mandarin", "我爱你"),
    ("🇧🇷", "Portuguese", "Eu amo-te"),
    ("🇷🇺", "Russian", "Я тебя люблю"),
    ("🇬🇷", "Greek", "Σ' αγαπώ"),
    ("🇸🇦", "Arabic", "أحبك"),
    ("🇮🇳", "Hindi", "मैं तुमसे प्यार करता हूँ"),
    ("🇳🇱", "Dutch", "Ik hou van jou"),
    ("🇸🇪", "Swedish", "Jag älskar dig"),
    ("🇵🇱", "Polish", "Kocham Cię"),
    ("🇵🇭", "Tagalog", "Mahal kita"),
    ("🇻🇳", "Vietnamese", "Anh yêu em"),
    ("🇮🇪", "Irish", "Tá grá agam ort")
]

print("💖 Kalpten Kalbe 20 Dil Projesi 💖\\n")
for flag, lang, phrase in love_languages:
    print(f"{flag} {lang} -> {phrase}")
`;

        function renderCards() {
            const grid = document.getElementById('heart-container-grid');
            grid.innerHTML = '';

            languagesData.forEach((item) => {
                const card = document.createElement('div');
                card.className = 'glass-card heart-item p-4 rounded-2xl flex flex-col items-center justify-center text-center cursor-pointer group relative';
                card.onclick = (e) => handleCardClick(item, card, e);

                card.innerHTML = `
                    <div class="text-2xl mb-1 filter drop-shadow">${item.flag}</div>
                    <div class="text-xs font-semibold text-rose-300 mb-0.5">${item.lang}</div>
                    <div class="text-sm sm:text-base font-bold text-white group-hover:text-rose-300 transition-colors">${item.phrase}</div>
                    <div class="text-[10px] text-gray-400 italic mt-1">"${item.phonetic}"</div>
                `;
                grid.appendChild(card);
            });
        }

        function handleCardClick(item, cardElement, event) {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                const utterance = new SpeechSynthesisUtterance(item.phrase);
                utterance.lang = item.lang === 'Türkçe' ? 'tr-TR' : 'en-US';
                window.speechSynthesis.speak(utterance);
            }

            const rect = cardElement.getBoundingClientRect();
            const x = (rect.left + rect.width / 2) / window.innerWidth;
            const y = (rect.top + rect.height / 2) / window.innerHeight;

            confetti({
                particleCount: 35,
                spread: 70,
                origin: { x: x, y: y },
                colors: ['#f43f5e', '#ec4899', '#fda4af', '#fb7185']
            });

            cardElement.classList.add('scale-95', 'border-rose-500');
            setTimeout(() => {
                cardElement.classList.remove('scale-95', 'border-rose-500');
            }, 200);
        }

        function triggerGlobalCelebration() {
            const duration = 3 * 1000;
            const end = Date.now() + duration;

            (function frame() {
                confetti({
                    particleCount: 5,
                    angle: 60,
                    spread: 55,
                    origin: { x: 0 },
                    colors: ['#f43f5e', '#ec4899', '#ffffff']
                });
                confetti({
                    particleCount: 5,
                    angle: 120,
                    spread: 55,
                    origin: { x: 1 },
                    colors: ['#f43f5e', '#ec4899', '#ffffff']
                });

                if (Date.now() < end) {
                    requestAnimationFrame(frame);
                }
            }());
        }

        function createFloatingHearts() {
            const container = document.getElementById('hearts-container');
            setInterval(() => {
                if (container.childElementCount > 25) return;
                const heart = document.createElement('div');
                heart.className = 'floating-heart';
                heart.innerHTML = '<i class="fa-solid fa-heart"></i>';
                
                const size = Math.random() * 18 + 12;
                const leftPos = Math.random() * 100;
                const animDuration = Math.random() * 4 + 4;
                const opacity = Math.random() * 0.5 + 0.3;

                heart.style.fontSize = `${size}px`;
                heart.style.left = `${leftPos}%`;
                heart.style.animationDuration = `${animDuration}s`;
                heart.style.opacity = opacity;

                container.appendChild(heart);
                setTimeout(() => heart.remove(), animDuration * 1000);
            }, 400);
        }

        function togglePythonModal(show) {
            const modal = document.getElementById('python-modal');
            if (show) {
                document.getElementById('python-code-content').textContent = pythonCodeString;
                modal.classList.remove('hidden');
                setTimeout(() => modal.classList.remove('opacity-0'), 10);
            } else {
                modal.classList.add('opacity-0');
                setTimeout(() => modal.classList.add('hidden'), 300);
            }
        }

        function copyPythonCode() {
            navigator.clipboard.writeText(pythonCodeString).then(() => {
                alertBox("Python kaynak kodu kopyalandı! 📋✨");
            });
        }

        function alertBox(message) {
            const toast = document.createElement('div');
            toast.className = 'fixed bottom-5 left-1/2 transform -translate-x-1/2 z-50 glass-card bg-rose-950/90 text-white px-6 py-3 rounded-2xl shadow-2xl border border-rose-500/40 text-sm flex items-center gap-3';
            toast.innerHTML = `<i class="fa-solid fa-circle-check text-rose-400 text-lg"></i> <span>${message}</span>`;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                toast.style.transition = 'opacity 0.5s ease';
                setTimeout(() => toast.remove(), 500);
            }, 3000);
        }

        window.onload = function() {
            renderCards();
            createFloatingHearts();
        };
    </script>
</body>
</html>

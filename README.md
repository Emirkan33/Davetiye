<!DOCTYPE html>
<html lang="en">
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

        /* Glassmorphism effects */
        .glass-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
        }

        .glass-card:hover {
            background: rgba(255, 255, 255, 0.09);
            border-color: rgba(244, 63, 94, 0.4);
            box-shadow: 0 12px 40px 0 rgba(244, 63, 94, 0.2);
        }

        /* Neon Glow animations */
        @keyframes pulse-glow {
            0%, 100% { text-shadow: 0 0 10px rgba(244, 63, 94, 0.6), 0 0 20px rgba(244, 63, 94, 0.4); }
            50% { text-shadow: 0 0 20px rgba(244, 63, 94, 0.9), 0 0 30px rgba(236, 72, 153, 0.8); }
        }

        .neon-title {
            animation: pulse-glow 3s infinite ease-in-out;
        }

        /* Floating Hearts Animation */
        @keyframes floatUp {
            0% {
                transform: translateY(100vh) scale(0.5);
                opacity: 0;
            }
            20% {
                opacity: 0.8;
            }
            80% {
                opacity: 0.8;
            }
            100% {
                transform: translateY(-10vh) scale(1.2);
                opacity: 0;
            }
        }

        .floating-heart {
            position: absolute;
            color: rgba(244, 63, 94, 0.6);
            animation: floatUp 6s infinite linear;
            bottom: -20px;
            pointer-events: none;
            z-index: 1;
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0d0410;
        }
        ::-webkit-scrollbar-thumb {
            background: #e11d48;
            border-radius: 4px;
        }
    </style>
</head>
<body class="relative flex flex-col min-h-100vh selection:bg-rose-500 selection:text-white">

    <div id="hearts-container" class="absolute inset-0 overflow-hidden pointer-events-none z-0"></div>

    <header class="relative z-10 w-full max-w-6xl mx-auto px-4 py-6 flex flex-col sm:flex-row justify-between items-center gap-4">
        <div class="flex items-center gap-3">
            <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-rose-600 to-pink-500 flex items-center justify-center shadow-lg shadow-rose-500/30">
                <i class="fa-solid fa-heart text-white text-xl animate-pulse"></i>
            </div>
            <div>
                <h1 class="text-xl font-bold bg-gradient-to-r from-rose-400 via-pink-300 to-purple-400 bg-clip-text text-transparent">L'Amour Global</h1>
                <p class="text-xs text-rose-300/70">"I Love You" in 20 Languages</p>
            </div>
        </div>
        <div class="flex items-center gap-3">
            <button onclick="triggerGlobalCelebration()" class="px-4 py-2.5 rounded-xl bg-gradient-to-r from-rose-600 to-pink-600 hover:from-rose-500 hover:to-pink-500 text-white font-medium text-sm shadow-lg shadow-rose-600/30 transition-all duration-300 transform hover:scale-105 active:scale-95 flex items-center gap-2">
                <i class="fa-solid fa-wand-magic-sparkles"></i> Celebration Mode
            </button>
            <button onclick="togglePythonModal(true)" class="px-4 py-2.5 rounded-xl glass-card hover:bg-white/10 text-rose-200 font-medium text-sm transition-all duration-300 transform hover:scale-105 active:scale-95 flex items-center gap-2 border border-rose-500/30">
                <i class="fa-brands fa-python text-rose-400"></i> Python Code
            </button>
        </div>
    </header>

    <main class="relative z-10 w-full max-w-6xl mx-auto px-4 flex-grow flex flex-col items-center justify-center my-8">
        <div class="text-center max-w-2xl mb-10">
            <h2 class="text-3xl sm:text-5xl font-extrabold text-white mb-4 tracking-tight neon-title">
                Expressions of Love
            </h2>
            <p class="text-sm sm:text-base text-gray-300/90 leading-relaxed">
                Explore how the most beautiful words are spoken across the globe. Click any card to hear pronunciation, reveal country details, and trigger mini heart animations!
            </p>
        </div>

        <div id="cards-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-5 w-full">
            <!-- Dynamically populated via JavaScript -->
        </div>
    </main>

    <footer class="relative z-10 w-full text-center py-6 text-xs text-gray-400 border-t border-white/5 mt-auto">
        <p>Crafted with endless love, modern web tech, and Python inspiration ❤️</p>
    </footer>

    <div id="python-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden transition-opacity duration-300 opacity-0">
        <div class="glass-card w-full max-w-3xl rounded-3xl p-6 border border-rose-500/30 shadow-2xl relative max-h-[90vh] flex flex-col">
            <div class="flex justify-between items-center pb-4 border-b border-white/10">
                <div class="flex items-center gap-3">
                    <div class="w-8 h-8 rounded-lg bg-blue-500/20 text-blue-400 flex items-center justify-center">
                        <i class="fa-brands fa-python text-lg"></i>
                    </div>
                    <h3 class="text-lg font-bold text-white">Python Source Code Structure</h3>
                </div>
                <button onclick="togglePythonModal(false)" class="w-8 h-8 rounded-full bg-white/5 hover:bg-white/10 flex items-center justify-center text-gray-400 hover:text-white transition-colors">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <div class="py-4 overflow-y-auto flex-grow font-mono text-xs sm:text-sm text-rose-100/90 bg-[#09020c]/80 p-4 rounded-xl border border-white/5">
                <pre><code id="python-code-content">            </div>
            <div class="pt-4 flex justify-between items-center border-t border-white/10">
                <span class="text-xs text-gray-400">Python 3.10+ Compatible Dictionary & Loop Structure</span>
                <button onclick="copyPythonCode()" class="px-4 py-2 rounded-xl bg-rose-600/80 hover:bg-rose-600 text-white text-xs font-semibold transition-all flex items-center gap-2">
                    <i class="fa-regular fa-copy"></i> Copy Code
                </button>
            </div>
        </div>
    </div>

    <script>
        // 20 Languages Data Set with Flag Emoji, Phrase, Translation, and Pronunciation Guide
        const languagesData = [
            { id: 1, lang: "English", country: "United States / UK", flag: "🇺🇸", phrase: "I love you", phonetic: "Eye luv yoo" },
            { id: 2, lang: "Turkish", country: "Turkey", flag: "🇹🇷", phrase: "Seni seviyorum", phonetic: "Seh-nee seh-vee-yo-rum" },
            { id: 3, lang: "French", country: "France", flag: "🇫🇷", phrase: "Je t'aime", phonetic: "Zhuh tem" },
            { id: 4, lang: "Spanish", country: "Spain / Latin America", flag: "🇪🇸", phrase: "Te quiero / Te amo", phonetic: "Teh kyeh-ro / Te teh ah-mo" },
            { id: 5, lang: "German", country: "Germany", flag: "🇩🇪", phrase: "Ich liebe dich", phonetic: "Ish lee-buh dish" },
            { id: 6, lang: "Italian", country: "Italy", flag: "🇮🇹", phrase: "Ti amo", phonetic: "Tee ah-mo" },
            { id: 7, lang: "Japanese", country: "Japan", flag: "🇯🇵", phrase: "愛してる (Aishiteru)", phonetic: "Ai-shi-te-ru" },
            { id: 8, lang: "Korean", country: "South Korea", flag: "🇰🇷", phrase: "사랑해 (Saranghae)", phonetic: "Sah-rang-hae" },
            { id: 9, lang: "Mandarin Chinese", country: "China", flag: "🇨🇳", phrase: "我爱你 (Wǒ ài nǐ)", phonetic: "Woh eye nee" },
            { id: 10, lang: "Portuguese", country: "Portugal / Brazil", flag: "🇧🇷", phrase: "Eu amo-te / Te amo", phonetic: "Eh-oo ah-mo-teh" },
            { id: 11, lang: "Russian", country: "Russia", flag: "🇷🇺", phrase: "Я тебя люблю", phonetic: "Ya tyeb-ya lyub-lyu" },
            { id: 12, lang: "Greek", country: "Greece", flag: "🇬🇷", phrase: "Σ' αγαπώ (S' agapo)", phonetic: "Sah-gah-poh" },
            { id: 13, lang: "Arabic", country: "Middle East / North Africa", flag: "🇸🇦", phrase: "أحبك (Uhibbuka)", phonetic: "Oo-hib-bu-ka" },
            { id: 14, lang: "Hindi", country: "India", flag: "🇮🇳", phrase: "मैं तुमसे प्यार करता हूँ", phonetic: "Main tumse pyaar karta hoon" },
            { id: 15, lang: "Dutch", country: "Netherlands", flag: "🇳🇱", phrase: "Ik hou van jou", phonetic: "Ik how vahn yow" },
            { id: 16, lang: "Swedish", country: "Sweden", flag: "🇸🇪", phrase: "Jag älskar dig", phonetic: "Yahg el-skar day" },
            { id: 17, lang: "Polish", country: "Poland", flag: "🇵🇱", phrase: "Kocham Cię", phonetic: "Ko-ham chye" },
            { id: 18, lang: "Tagalog", country: "Philippines", flag: "🇵🇭", phrase: "Mahal kita", phonetic: "Ma-hal kee-ta" },
            { id: 19, lang: "Vietnamese", country: "Vietnam", flag: "🇻🇳", phrase: "Anh yêu em / Em yêu anh", phonetic: "Anh yew em" },
            { id: 20, lang: "Irish Gaelic", country: "Ireland", flag: "🇮🇪", phrase: "Tá grá agam ort", phonetic: "Taw graw ah-gum urt" }
        ];

        // Python source code representation for the modal
        const pythonCodeString = `# -*- coding: utf-8 -*-
\"\"\"
I Love You in 20 Different Languages
Written in Python with a structured dictionary and voice/display simulation.
\"\"\"

import time
import sys

# Dictionary containing 20 languages, countries, and romantic phrases
love_languages = {
    1: {"lang": "English", "country": "United Kingdom/USA", "phrase": "I love you"},
    2: {"lang": "Turkish", "country": "Turkey", "phrase": "Seni seviyorum"},
    3: {"lang": "French", "country": "France", "phrase": "Je t'aime"},
    4: {"lang": "Spanish", "country": "Spain", "phrase": "Te amo"},
    5: {"lang": "German", "country": "Germany", "phrase": "Ich liebe dich"},
    6: {"lang": "Italian", "country": "Italy", "phrase": "Ti amo"},
    7: {"lang": "Japanese", "country": "Japan", "phrase": "愛してる (Aishiteru)"},
    8: {"lang": "Korean", "country": "South Korea", "phrase": "사랑해 (Saranghae)"},
    9: {"lang": "Mandarin", "country": "China", "phrase": "我爱你 (Wǒ ài nǐ)"},
    10: {"lang": "Portuguese", "country": "Brazil/Portugal", "phrase": "Eu amo-te"},
    11: {"lang": "Russian", "country": "Russia", "phrase": "Я тебя люблю"},
    12: {"lang": "Greek", "country": "Greece", "phrase": "Σ' αγαπώ"},
    13: {"lang": "Arabic", "country": "Arab World", "phrase": "أحبك (Uhibbuka)"},
    14: {"lang": "Hindi", "country": "India", "phrase": "मैं तुमसे प्यार करता हूँ"},
    15: {"lang": "Dutch", "country": "Netherlands", "phrase": "Ik hou van jou"},
    16: {"lang": "Swedish", "country": "Sweden", "phrase": "Jag älskar dig"},
    17: {"lang": "Polish", "country": "Poland", "phrase": "Kocham Cię"},
    18: {"lang": "Tagalog", "country": "Philippines", "phrase": "Mahal kita"},
    19: {"lang": "Vietnamese", "country": "Vietnam", "phrase": "Anh yêu em"},
    20: {"lang": "Irish", "country": "Ireland", "phrase": "Tá grá agam ort"}
}

def express_love_globally():
    print("💖 Starting Global Expression of Love... 💖\\n")
    for index, data in love_languages.items():
        lang = data["lang"]
        phrase = data["phrase"]
        country = data["country"]
        
        # Format output cleanly
        print(f"[{index:02d}] {lang} ({country}): \\033[91m{phrase}\\033[0m")
        time.sleep(0.3)  # Gentle pause for emotional impact
        
    print("\\n✨ Love transcends all language barriers! ✨")

if __name__ == "__main__":
    express_love_globally()
`;

        // Render Cards Grid
        function renderCards() {
            const grid = document.getElementById('cards-grid');
            grid.innerHTML = '';

            languagesData.forEach((item) => {
                const card = document.createElement('div');
                card.className = 'glass-card rounded-2xl p-5 flex flex-col justify-between transition-all duration-300 cursor-pointer group relative overflow-hidden';
                card.onclick = (e) => handleCardClick(item, card, e);

                card.innerHTML = `
                    <div class="flex justify-between items-start mb-3">
                        <span class="text-3xl filter drop-shadow-md">${item.flag}</span>
                        <span class="text-xs font-semibold px-2.5 py-1 rounded-full bg-rose-500/10 text-rose-300 border border-rose-500/20 group-hover:bg-rose-500/20 transition-colors">
                            #${item.id}
                        </span>
                    </div>
                    <div>
                        <h4 class="text-sm font-medium text-gray-400 mb-1">${item.lang} <span class="text-xs opacity-60">(${item.country})</span></h4>
                        <p class="text-lg sm:text-xl font-bold text-white group-hover:text-rose-300 transition-colors mb-2">${item.phrase}</p>
                        <p class="text-xs text-rose-300/80 italic flex items-center gap-1.5">
                            <i class="fa-solid fa-volume-high opacity-70"></i> <span>"${item.phonetic}"</span>
                        </p>
                    </div>
                    <div class="mt-4 pt-3 border-t border-white/5 flex justify-between items-center text-xs text-gray-400">
                        <span class="group-hover:text-rose-400 transition-colors">Click to speak & heart ✨</span>
                        <i class="fa-solid fa-heart text-rose-500/40 group-hover:text-rose-500 transition-colors transform group-hover:scale-125"></i>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        // Handle Card Interaction (Speech + Mini Confetti Burst + Sparkle)
        function handleCardClick(item, cardElement, event) {
            // Trigger browser speech synthesis
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel(); // Stop previous utterance
                const utterance = new SpeechSynthesisUtterance(item.phrase);
                // Map basic language codes if possible or default
                if (item.lang === 'French') utterance.lang = 'fr-FR';
                else if (item.lang === 'Spanish') utterance.lang = 'es-ES';
                else if (item.lang === 'Turkish') utterance.lang = 'tr-TR';
                else if (item.lang === 'German') utterance.lang = 'de-DE';
                else if (item.lang === 'Italian') utterance.lang = 'it-IT';
                else if (item.lang === 'Japanese') utterance.lang = 'ja-JP';
                else if (item.lang === 'Korean') utterance.lang = 'ko-KR';
                else if (item.lang === 'Mandarin Chinese') utterance.lang = 'zh-CN';
                else if (item.lang === 'Russian') utterance.lang = 'ru-RU';
                else if (item.lang === 'Portuguese') utterance.lang = 'pt-BR';
                else if (item.lang === 'Dutch') utterance.lang = 'nl-NL';
                else if (item.lang === 'Polish') utterance.lang = 'pl-PL';
                else if (item.lang === 'Swedish') utterance.lang = 'sv-SE';
                else utterance.lang = 'en-US';

                window.speechSynthesis.speak(utterance);
            }

            // Confetti burst from click position
            const rect = cardElement.getBoundingClientRect();
            const x = (rect.left + rect.width / 2) / window.innerWidth;
            const y = (rect.top + rect.height / 2) / window.innerHeight;

            confetti({
                particleCount: 30,
                spread: 60,
                origin: { x: x, y: y },
                colors: ['#f43f5e', '#ec4899', '#fda4af', '#fb7185']
            });

            // Card click bounce effect
            cardElement.classList.add('scale-95', 'border-rose-500');
            setTimeout(() => {
                cardElement.classList.remove('scale-95', 'border-rose-500');
            }, 200);
        }

        // Global Celebration Trigger
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

        // Background Floating Hearts Generator
        function createFloatingHearts() {
            const container = document.getElementById('hearts-container');
            const heartIcons = ['fa-heart', 'fa-solid fa-heart'];
            
            setInterval(() => {
                if (container.childElementCount > 25) return; // Limit active DOM nodes
                const heart = document.createElement('div');
                heart.className = 'floating-heart';
                heart.innerHTML = '<i class="fa-solid fa-heart"></i>';
                
                const size = Math.random() * 18 + 12; // 12px to 30px
                const leftPos = Math.random() * 100; // 0% to 100%
                const animDuration = Math.random() * 4 + 4; // 4s to 8s
                const opacity = Math.random() * 0.5 + 0.3;

                heart.style.fontSize = `${size}px`;
                heart.style.left = `${leftPos}%`;
                heart.style.animationDuration = `${animDuration}s`;
                heart.style.opacity = opacity;

                container.appendChild(heart);

                setTimeout(() => {
                    heart.remove();
                }, animDuration * 1000);
            }, 400);
        }

        // Python Modal Toggle
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

        // Copy Python Code
        function copyPythonCode() {
            const code = pythonCodeString;
            const textArea = document.createElement('textarea');
            textArea.value = code;
            document.body.appendChild(textArea);
            textArea.select();
            try {
                document.execCommand('copy');
                alertBox("Python source code copied to clipboard successfully! 📋✨");
            } catch (err) {
                console.error('Failed to copy text', err);
            }
            document.body.removeChild(textArea);
        }

        // Custom non-blocking alert box replacement
        function alertBox(message) {
            const toast = document.createElement('div');
            toast.className = 'fixed bottom-5 left-1/2 transform -translate-x-1/2 z-50 glass-card bg-rose-950/90 text-white px-6 py-3 rounded-2xl shadow-2xl border border-rose-500/40 text-sm flex items-center gap-3 animate-bounce';
            toast.innerHTML = `<i class="fa-solid fa-circle-check text-rose-400 text-lg"></i> <span>${message}</span>`;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                toast.style.transition = 'opacity 0.5s ease';
                setTimeout(() => toast.remove(), 500);
            }, 3000);
        }

        // Initialize App on Window Load
        window.onload = function() {
            renderCards();
            createFloatingHearts();
        };
    </script>
</body>
</html>

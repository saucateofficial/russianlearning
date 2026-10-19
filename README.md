<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rusça Cinsiyet ve Kelime Oyunu</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        .perspective-1000 { perspective: 1000px; }
        .transform-style-3d { transform-style: preserve-3d; }
        .backface-hidden { backface-visibility: hidden; }
        .rotate-y-180 { transform: rotateY(180deg); }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-screen flex flex-col font-sans">
    
    <!-- Header -->
    <header class="bg-slate-800 border-b border-slate-700 py-4 px-6 sticky top-0 z-50 shadow-md">
        <div class="max-w-6xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4">
            <div>
                <h1 class="text-xl font-bold text-blue-400 flex items-center gap-2">
                    🇷🇺 Rusça Cinsiyet ve Kelime Çalışma Alanı
                </h1>
                <p class="text-xs text-slate-400">Flashcard, Eşleştirme ve Test Modülü</p>
            </div>
            <nav class="flex gap-2">
                <button onclick="switchTab('flashcards')" id="btn-flashcards" class="px-4 py-2 rounded-lg text-sm font-medium bg-blue-600 text-white transition shadow">Flashcards</button>
                <button onclick="switchTab('matching')" id="btn-matching" class="px-4 py-2 rounded-lg text-sm font-medium bg-slate-700 text-slate-300 hover:bg-slate-600 transition">Eşleştirme Oyunu</button>
                <button onclick="switchTab('quiz')" id="btn-quiz" class="px-4 py-2 rounded-lg text-sm font-medium bg-slate-700 text-slate-300 hover:bg-slate-600 transition">Test</button>
            </nav>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-4xl w-full mx-auto p-4 sm:p-6 flex flex-col justify-center">

        <!-- FLASHCARDS SECTION -->
        <section id="section-flashcards" class="tab-content flex flex-col items-center gap-6">
            <div class="w-full flex justify-between items-center text-sm text-slate-400 px-2">
                <span id="fc-progress">Kart 1 / 60</span>
                <span class="bg-slate-800 px-3 py-1 rounded-full border border-slate-700">Çevirmek için karta tıklayın</span>
            </div>

            <!-- Card Element -->
            <div class="w-full max-w-md h-72 perspective-1000 cursor-pointer" onclick="flipCard()">
                <div id="flashcard-inner" class="relative w-full h-full duration-500 transform-style-3d shadow-xl rounded-2xl">
                    <!-- Front -->
                    <div class="absolute inset-0 w-full h-full bg-slate-800 border-2 border-slate-700 rounded-2xl flex flex-col items-center justify-center p-6 backface-hidden">
                        <span id="fc-gender" class="text-xs uppercase tracking-widest text-blue-400 mb-2 font-semibold">Eril (Он)</span>
                        <h2 id="fc-russian" class="text-4xl font-bold text-white mb-3 text-center">дом</h2>
                        <p id="fc-pronounce" class="text-lg text-slate-400 italic">[ dom ]</p>
                    </div>
                    <!-- Back -->
                    <div class="absolute inset-0 w-full h-full bg-slate-700 border-2 border-slate-600 rounded-2xl flex flex-col items-center justify-center p-6 backface-hidden rotate-y-180">
                        <span class="text-xs uppercase tracking-widest text-emerald-400 mb-2 font-semibold">Türkçe Anlamı</span>
                        <h2 id="fc-turkish" class="text-3xl font-bold text-white text-center">ev / bina</h2>
                    </div>
                </div>
            </div>

            <!-- Controls -->
            <div class="flex gap-4 w-full max-w-md">
                <button onclick="prevCard()" class="flex-1 bg-slate-800 hover:bg-slate-700 border border-slate-700 py-3 rounded-xl font-medium transition flex items-center justify-center gap-2">⬅ Önceki</button>
                <button onclick="nextCard()" class="flex-1 bg-blue-600 hover:bg-blue-500 py-3 rounded-xl font-medium transition flex items-center justify-center gap-2">Sonraki ➡</button>
            </div>
        </section>

        <!-- MATCHING GAME SECTION -->
        <section id="section-matching" class="tab-content hidden flex flex-col gap-6">
            <div class="flex justify-between items-center bg-slate-800 p-4 rounded-xl border border-slate-700">
                <div>
                    <h3 class="font-bold text-lg text-white">Kelime Eşleştirme Bulmacası</h3>
                    <p class="text-xs text-slate-400">Rusça kelimeleri doğru Türkçe anlamlarıyla eşleştir.</p>
                </div>
                <div class="text-right">
                    <span class="text-sm text-slate-400">Skor: <strong id="match-score" class="text-emerald-400">0</strong> / 6</span>
                    <button onclick="initMatchingGame()" class="block text-xs bg-slate-700 hover:bg-slate-600 px-3 py-1 rounded mt-1 text-slate-200 transition">Yeniden Başlat</button>
                </div>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div class="flex flex-col gap-3">
                    <h4 class="text-xs font-bold uppercase tracking-wider text-blue-400">Rusça Kelimeler</h4>
                    <div id="matching-russian-col" class="flex flex-col gap-2"></div>
                </div>
                <div class="flex flex-col gap-3">
                    <h4 class="text-xs font-bold uppercase tracking-wider text-emerald-400">Türkçe Anlamları</h4>
                    <div id="matching-turkish-col" class="flex flex-col gap-2"></div>
                </div>
            </div>
        </section>

        <!-- QUIZ SECTION -->
        <section id="section-quiz" class="tab-content hidden flex flex-col gap-6">
            <div id="quiz-container" class="bg-slate-800 border border-slate-700 rounded-2xl p-6 shadow-lg">
                <div class="flex justify-between items-center mb-6 border-b border-slate-700 pb-4">
                    <span id="quiz-progress" class="text-sm font-medium text-slate-400">Soru 1 / 10</span>
                    <span id="quiz-score-badge" class="text-sm font-semibold bg-blue-900/50 text-blue-300 px-3 py-1 rounded-full border border-blue-800">Doğru: 0</span>
                </div>

                <h3 id="quiz-question" class="text-xl font-bold text-white mb-6">Rusça kelimenin Türkçe karşılığı nedir?</h3>

                <div id="quiz-options" class="grid grid-cols-1 gap-3 mb-6"></div>

                <div class="flex justify-end">
                    <button id="quiz-next-btn" onclick="nextQuizQuestion()" class="hidden bg-blue-600 hover:bg-blue-500 text-white px-6 py-2.5 rounded-xl font-medium transition">Sonraki Soru ➡</button>
                </div>
            </div>

            <!-- Quiz Result Card -->
            <div id="quiz-result" class="hidden bg-slate-800 border border-slate-700 rounded-2xl p-8 text-center flex flex-col items-center gap-4">
                <h3 class="text-2xl font-bold text-white">Test Tamamlandı! 🎉</h3>
                <p id="quiz-final-score" class="text-lg text-slate-300">Skorun: 10 / 10</p>
                <button onclick="restartQuiz()" class="bg-blue-600 hover:bg-blue-500 text-white px-6 py-2.5 rounded-xl font-medium transition">Testi Yeniden Başlat</button>
            </div>
        </section>

    </main>

    <footer class="text-center py-4 text-xs text-slate-500 border-t border-slate-800">
        Resimli Kitap Kelimeler Seti &copy; 2026
    </footer>

    <!-- Application Script -->
    <script>
        const vocabularyData = [
            { ru: "дом", pron: "dom", tr: "ev / bina", gender: "Eril (Он)" },
            { ru: "трамвай", pron: "tramvay", tr: "tramvay", gender: "Eril (Он)" },
            { ru: "спутник", pron: "sputnik", tr: "uydu", gender: "Eril (Он)" },
            { ru: "мальчик", pron: "mal'çik", tr: "erkek çocuk", gender: "Eril (Он)" },
            { ru: "карандаш", pron: "karandaş", tr: "kurşun kalem", gender: "Eril (Он)" },
            { ru: "нож", pron: "noj", tr: "bıçak", gender: "Eril (Он)" },
            { ru: "мяч", pron: "myaç", tr: "top", gender: "Eril (Он)" },
            { ru: "хлеб", pron: "hleb", tr: "ekmek", gender: "Eril (Он)" },
            { ru: "остров", pron: "ostrov", tr: "ada", gender: "Eril (Он)" },
            { ru: "поезд", pron: "poyezd", tr: "tren", gender: "Eril (Он)" },
            { ru: "стол", pron: "stol", tr: "masa", gender: "Eril (Он)" },
            { ru: "костюм", pron: "kostyum", tr: "takım elbise", gender: "Eril (Он)" },
            { ru: "магазин", pron: "magazin", tr: "mağaza", gender: "Eril (Он)" },
            { ru: "автобус", pron: "avtobus", tr: "otobüs", gender: "Eril (Он)" },
            { ru: "космонавт", pron: "kosmonavt", tr: "astronot", gender: "Eril (Он)" },
            { ru: "музей", pron: "muzey", tr: "müze", gender: "Eril (Он)" },
            { ru: "чай", pron: "çay", tr: "çay", gender: "Eril (Он)" },
            { ru: "вокзал", pron: "vokzal", tr: "tren garı", gender: "Eril (Он)" },
            { ru: "врач", pron: "vraç", tr: "doktor", gender: "Eril (Он)" },
            { ru: "картина", pron: "kartina", tr: "tablo / resim", gender: "Dişil (Она)" },
            { ru: "семья", pron: "sem'ya", tr: "aile", gender: "Dişil (Она)" },
            { ru: "учительница", pron: "uçitel'nitsa", tr: "kadın öğretmen", gender: "Dişil (Она)" },
            { ru: "девочка", pron: "devoçka", tr: "kız çocuk", gender: "Dişil (Она)" },
            { ru: "рыба", pron: "ryba", tr: "balık", gender: "Dişil (Она)" },
            { ru: "книга", pron: "kniga", tr: "kitap", gender: "Dişil (Она)" },
            { ru: "доска", pron: "doska", tr: "yazı tahtası", gender: "Dişil (Она)" },
            { ru: "звезда", pron: "zvezda", tr: "yıldız", gender: "Dişil (Она)" },
            { ru: "женщина", pron: "jenşçina", tr: "kadın", gender: "Dişil (Она)" },
            { ru: "кухня", pron: "kuhnya", tr: "mutfak", gender: "Dişil (Она)" },
            { ru: "вода", pron: "voda", tr: "su", gender: "Dişil (Она)" },
            { ru: "комната", pron: "komnata", tr: "oda", gender: "Dişil (Она)" },
            { ru: "работа", pron: "rabota", tr: "iş / çalışma", gender: "Dişil (Она)" },
            { ru: "машина", pron: "maşina", tr: "araba", gender: "Dişil (Она)" },
            { ru: "страна", pron: "strana", tr: "ülke", gender: "Dişil (Она)" },
            { ru: "письмо", pron: "pis'mo", tr: "mektup", gender: "Nötr (Оно)" },
            { ru: "платье", pron: "plat'ye", tr: "elbise", gender: "Nötr (Оно)" },
            { ru: "окно", pron: "okno", tr: "pencere", gender: "Nötr (Оно)" },
            { ru: "кресло", pron: "kreslo", tr: "tekli koltuk", gender: "Nötr (Оно)" },
            { ru: "кольцо", pron: "kol'tso", tr: "yüzük", gender: "Nötr (Оно)" },
            { ru: "дерево", pron: "derevo", tr: "ağaç", gender: "Nötr (Оно)" },
            { ru: "яблоко", pron: "yabloko", tr: "elma", gender: "Nötr (Оно)" },
            { ru: "солнце", pron: "solntse", tr: "güneş", gender: "Nötr (Оно)" },
            { ru: "море", pron: "more", tr: "deniz", gender: "Nötr (Оно)" },
            { ru: "время", pron: "vremya", tr: "zaman", gender: "Nötr (-мя)" },
            { ru: "имя", pron: "imya", tr: "ad / isim", gender: "Nötr (-мя)" },
            { ru: "учитель", pron: "uçitel'", tr: "öğretmen", gender: "Eril (-тель)" },
            { ru: "портфель", pron: "portfel'", tr: "evrak çantası", gender: "Eril (Он)" },
            { ru: "словарь", pron: "slovar'", tr: "sözlük", gender: "Eril (Он)" },
            { ru: "дождь", pron: "dojd'", tr: "yağmur", gender: "Eril (Он)" },
            { ru: "день", pron: "den'", tr: "gün", gender: "Eril (Он)" },
            { ru: "мать", pron: "mat'", tr: "anne", gender: "Dişil (Она)" },
            { ru: "дочь", pron: "doç'", tr: "kız evlat", gender: "Dişil (Она)" },
            { ru: "дверь", pron: "dver'", tr: "kapı", gender: "Dişil (Она)" },
            { ru: "тетрадь", pron: "tetrad'", tr: "defter", gender: "Dişil (Она)" },
            { ru: "ночь", pron: "noç'", tr: "gece", gender: "Dişil (Она)" },
            { ru: "любовь", pron: "lyubov'", tr: "aşk / sevgi", gender: "Dişil (Она)" },
            { ru: "папа", pron: "papa", tr: "baba", gender: "Eril (Он - İstisna)" },
            { ru: "дедушка", pron: "deduşka", tr: "dede", gender: "Eril (Он - İstisna)" },
            { ru: "пальто", pron: "pal'to", tr: "palto", gender: "Nötr (Yabancı / Değişmez)" },
            { ru: "кино", pron: "kino", tr: "sinema", gender: "Nötr (Yabancı / Değişmez)" }
        ];

        // Tab Switcher
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById('section-' + tabId).classList.remove('hidden');

            ['flashcards', 'matching', 'quiz'].forEach(t => {
                const btn = document.getElementById('btn-' + t);
                if (t === tabId) {
                    btn.className = "px-4 py-2 rounded-lg text-sm font-medium bg-blue-600 text-white transition shadow";
                } else {
                    btn.className = "px-4 py-2 rounded-lg text-sm font-medium bg-slate-700 text-slate-300 hover:bg-slate-600 transition";
                }
            });

            if (tabId === 'matching' && matchItems.length === 0) {
                initMatchingGame();
            }
            if (tabId === 'quiz' && quizQuestions.length === 0) {
                initQuiz();
            }
        }

        // --- FLASHCARD LOGIC ---
        let currentCardIndex = 0;
        let isFlipped = false;

        function updateFlashcard() {
            const card = vocabularyData[currentCardIndex];
            document.getElementById('fc-russian').innerText = card.ru;
            document.getElementById('fc-pronounce').innerText = `[ ${card.pron} ]`;
            document.getElementById('fc-turkish').innerText = card.tr;
            document.getElementById('fc-gender').innerText = card.gender;
            document.getElementById('fc-progress').innerText = `Kart ${currentCardIndex + 1} / ${vocabularyData.length}`;
            
            if (isFlipped) {
                flipCard();
            }
        }

        function flipCard() {
            isFlipped = !isFlipped;
            const inner = document.getElementById('flashcard-inner');
            if (isFlipped) {
                inner.style.transform = 'rotateY(180deg)';
            } else {
                inner.style.transform = 'rotateY(0deg)';
            }
        }

        function nextCard() {
            currentCardIndex = (currentCardIndex + 1) % vocabularyData.length;
            updateFlashcard();
        }

        function prevCard() {
            currentCardIndex = (currentCardIndex - 1 + vocabularyData.length) % vocabularyData.length;
            updateFlashcard();
        }

        // --- MATCHING GAME LOGIC ---
        let matchItems = [];
        let selectedRussian = null;
        let selectedTurkish = null;
        let matchedCount = 0;

        function initMatchingGame() {
            matchedCount = 0;
            document.getElementById('match-score').innerText = matchedCount;
            
            const shuffled = [...vocabularyData].sort(() => 0.5 - Math.random());
            matchItems = shuffled.slice(0, 6);

            const ruCol = document.getElementById('matching-russian-col');
            const trCol = document.getElementById('matching-turkish-col');
            ruCol.innerHTML = '';
            trCol.innerHTML = '';

            const ruShuffled = [...matchItems].sort(() => 0.5 - Math.random());
            const trShuffled = [...matchItems].sort(() => 0.5 - Math.random());

            ruShuffled.forEach(item => {
                const btn = document.createElement('button');
                btn.className = "w-full p-3 bg-slate-800 hover:bg-slate-700 border border-slate-700 rounded-xl text-left font-medium transition flex justify-between items-center";
                btn.innerHTML = `<span>${item.ru}</span> <span class="text-xs text-slate-400">[${item.pron}]</span>`;
                btn.onclick = () => selectRussian(item, btn);
                ruCol.appendChild(btn);
            });

            trShuffled.forEach(item => {
                const btn = document.createElement('button');
                btn.className = "w-full p-3 bg-slate-800 hover:bg-slate-700 border border-slate-700 rounded-xl text-left font-medium transition";
                btn.innerText = item.tr;
                btn.onclick = () => selectTurkish(item, btn);
                trCol.appendChild(btn);
            });
        }

        let activeRuBtn = null;
        let activeTrBtn = null;
        let currentRuItem = null;
        let currentTrItem = null;

        function selectRussian(item, btn) {
            if (btn.classList.contains('bg-emerald-900/50')) return;
            if (activeRuBtn) activeRuBtn.classList.remove('border-blue-500', 'bg-slate-700');
            activeRuBtn = btn;
            currentRuItem = item;
            btn.classList.add('border-blue-500', 'bg-slate-700');
            checkMatch();
        }

        function selectTurkish(item, btn) {
            if (btn.classList.contains('bg-emerald-900/50')) return;
            if (activeTrBtn) activeTrBtn.classList.remove('border-emerald-500', 'bg-slate-700');
            activeTrBtn = btn;
            currentTrItem = item;
            btn.classList.add('border-emerald-500', 'bg-slate-700');
            checkMatch();
        }

        function checkMatch() {
            if (currentRuItem && currentTrItem) {
                if (currentRuItem.ru === currentTrItem.ru) {
                    activeRuBtn.className = "w-full p-3 bg-emerald-900/30 border border-emerald-600 rounded-xl text-left font-medium text-emerald-300 opacity-75 cursor-default flex justify-between items-center";
                    activeTrBtn.className = "w-full p-3 bg-emerald-900/30 border border-emerald-600 rounded-xl text-left font-medium text-emerald-300 opacity-75 cursor-default";
                    matchedCount++;
                    document.getElementById('match-score').innerText = matchedCount;

                    if (matchedCount === 6) {
                        setTimeout(() => {
                            alert("Tebrikler! Tüm kelimeleri başarıyla eşleştirdin! 🎉");
                            initMatchingGame();
                        }, 300);
                    }
                } else {
                    activeRuBtn.classList.remove('border-blue-500', 'bg-slate-700');
                    activeTrBtn.classList.remove('border-emerald-500', 'bg-slate-700');
                }
                activeRuBtn = null;
                activeTrBtn = null;
                currentRuItem = null;
                currentTrItem = null;
            }
        }

        // --- QUIZ LOGIC ---
        let quizQuestions = [];
        let currentQuizIndex = 0;
        let quizScore = 0;
        let answered = false;

        function initQuiz() {
            currentQuizIndex = 0;
            quizScore = 0;
            answered = false;
            document.getElementById('quiz-result').classList.add('hidden');
            document.getElementById('quiz-container').classList.remove('hidden');

            const shuffled = [...vocabularyData].sort(() => 0.5 - Math.random());
            quizQuestions = shuffled.slice(0, 10).map(item => {
                const incorrects = vocabularyData.filter(v => v.tr !== item.tr).sort(() => 0.5 - Math.random()).slice(0, 3).map(v => v.tr);
                const options = [...incorrects, item.tr].sort(() => 0.5 - Math.random());
                return {
                    ru: item.ru,
                    pron: item.pron,
                    gender: item.gender,
                    correct: item.tr,
                    options: options
                };
            });

            loadQuizQuestion();
        }

        function loadQuizQuestion() {
            answered = false;
            const q = quizQuestions[currentQuizIndex];
            document.getElementById('quiz-progress').innerText = `Soru ${currentQuizIndex + 1} / 10`;
            document.getElementById('quiz-score-badge').innerText = `Doğru: ${quizScore}`;
            document.getElementById('quiz-question').innerHTML = `"<span class="text-blue-400">${q.ru}</span>" <span class="text-xs text-slate-400">([${q.pron}] - ${q.gender})</span> kelimesinin Türkçe karşılığı nedir?`;
            
            const optionsContainer = document.getElementById('quiz-options');
            optionsContainer.innerHTML = '';

            q.options.forEach(opt => {
                const btn = document.createElement('button');
                btn.className = "w-full p-4 bg-slate-700/50 hover:bg-slate-700 border border-slate-600 rounded-xl font-medium text-left transition text-white";
                btn.innerText = opt;
                btn.onclick = () => selectQuizOption(btn, opt, q.correct);
                optionsContainer.appendChild(btn);
            });

            document.getElementById('quiz-next-btn').classList.add('hidden');
        }

        function selectQuizOption(btn, selected, correct) {
            if (answered) return;
            answered = true;

            const buttons = document.getElementById('quiz-options').children;
            for (let b of buttons) {
                if (b.innerText === correct) {
                    b.className = "w-full p-4 bg-emerald-900/60 border border-emerald-500 rounded-xl font-medium text-left text-white";
                } else if (b === btn && selected !== correct) {
                    b.className = "w-full p-4 bg-rose-900/60 border border-rose-500 rounded-xl font-medium text-left text-white";
                } else {
                    b.className = "w-full p-4 bg-slate-800/40 border border-slate-700/50 rounded-xl font-medium text-left text-slate-400";
                }
            }

            if (selected === correct) {
                quizScore++;
                document.getElementById('quiz-score-badge').innerText = `Doğru: ${quizScore}`;
            }

            document.getElementById('quiz-next-btn').classList.remove('hidden');
        }

        function nextQuizQuestion() {
            currentQuizIndex++;
            if (currentQuizIndex < quizQuestions.length) {
                loadQuizQuestion();
            } else {
                document.getElementById('quiz-container').classList.add('hidden');
                document.getElementById('quiz-result').classList.remove('hidden');
                document.getElementById('quiz-final-score').innerText = `Skorun: ${quizScore} / 10`;
            }
        }

        function restartQuiz() {
            initQuiz();
        }
    </script>
</body>
</html>

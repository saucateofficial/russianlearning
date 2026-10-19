<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rusça Kelime ve Cümle Defterim</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        .perspective-1000 { perspective: 1000px; }
        .transform-style-3d { transform-style: preserve-3d; }
        .backface-hidden { backface-visibility: hidden; }
        .rotate-y-180 { transform: rotateY(180deg); }
        body {
            background-color: #0c0c0c;
            background-image: radial-gradient(circle at 50% 0%, #1a1a1a 0%, #0c0c0c 100%);
        }
    </style>
</head>
<body class="text-neutral-100 min-h-screen flex flex-col font-mono selection:bg-neutral-200 selection:text-black">
    
    <!-- Header / Navbar -->
    <header class="w-full max-w-4xl mx-auto p-4 sm:p-6 relative">
        <div class="bg-black border border-neutral-800 shadow-2xl rounded-2xl py-4 px-6 flex flex-col sm:flex-row justify-between items-center gap-4">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-white text-black flex items-center justify-center shadow-lg font-bold text-lg tracking-wider">RU</div>
                <div>
                    <h1 class="text-sm font-bold text-white tracking-widest uppercase">Rusça Defterim</h1>
                    <p class="text-[11px] text-neutral-400">Notlar, Kelimeler ve Alıştırmalar</p>
                </div>
            </div>
            
            <!-- Navigation Tabs -->
            <nav class="flex gap-2 bg-neutral-950 p-1.5 rounded-xl border border-neutral-800">
                <button onclick="switchTab('flashcards')" id="btn-flashcards" class="px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all bg-white text-black shadow-lg">Flashcards</button>
                <button onclick="switchTab('matching')" id="btn-matching" class="px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all text-neutral-400 hover:text-white hover:bg-neutral-900">Eşleştirme</button>
                <button onclick="switchTab('quiz')" id="btn-quiz" class="px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all text-neutral-400 hover:text-white hover:bg-neutral-900">Test</button>
            </nav>
        </div>

        <!-- Gramer Notları Açılır Buton ve Panel (Sağ Üst Köşe) -->
        <div class="absolute top-6 right-6 z-50 sm:block hidden">
            <button onclick="toggleNotes()" class="bg-white text-black border border-neutral-700 px-3 py-1.5 rounded-lg text-xs font-bold uppercase tracking-wider shadow-md hover:bg-neutral-200 transition">📌 Gramer Notları</button>
            <div id="notesPanel" class="hidden absolute right-0 mt-2 w-80 bg-black border border-neutral-800 p-4 rounded-xl shadow-2xl text-xs text-neutral-300 space-y-3 z-50">
                <div class="flex justify-between items-center border-b border-neutral-800 pb-2">
                    <span class="font-bold text-white uppercase tracking-wider">Defter Notları</span>
                    <button onclick="toggleNotes()" class="text-neutral-500 hover:text-white font-bold">✕</button>
                </div>
                <ul class="space-y-2 max-h-60 overflow-y-auto pr-1">
                    <li><strong>Nötr Ek Kuralı:</strong> <em>-o</em> ile bitenler çoğulda <em>-a</em> olur; <em>-e</em> ile bitenler çoğulda <em>-я</em> olur[span_0](start_span)[span_0](end_span).</li>
                    <li><strong>Vurgu Değişimi:</strong> Kelimeler çoğul yapılırken vurgunun yeri (sesin yükseldiği hece) değişebilir (Örn: стол ➔ столы)[span_1](start_span)[span_1](end_span).</li>
                    <li><strong>Tablo Doldurma (-и / -ы):</strong> -а / -я ile biten dişil kelimeler çoğulda -и ekini alır[span_2](start_span)[span_2](end_span).</li>
                    <li><strong>İşaret Zamiri (Этo):</strong> Tekilde "Bu bir..." anlamındayken çoğulda "Bunlar..." anlamına döner ve isimler de çoğul yapılır (Это карандаш ➔ Это карандаши)[span_3](start_span)[span_3](end_span)[span_4](start_span)[span_4](end_span).</li>
                </ul>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-4xl w-full mx-auto p-4 sm:p-6 flex flex-col justify-center">

        <!-- FLASHCARDS SECTION -->
        <section id="section-flashcards" class="tab-content flex flex-col items-center gap-6">
            <div class="w-full flex justify-between items-center text-xs text-neutral-400 px-2 font-medium">
                <span id="fc-progress" class="bg-black border border-neutral-800 px-3 py-1.5 rounded-lg shadow">Kart 1 / 150</span>
                <span class="bg-black border border-neutral-800 px-3 py-1.5 rounded-lg shadow">Çevirmek için karta tıkla</span>
            </div>

            <!-- Card Element -->
            <div class="w-full max-w-md h-72 perspective-1000 cursor-pointer group" onclick="flipCard()">
                <div id="flashcard-inner" class="relative w-full h-full duration-500 transform-style-3d shadow-2xl rounded-2xl">
                    <!-- Front -->
                    <div class="absolute inset-0 w-full h-full bg-black border-2 border-neutral-800 rounded-2xl flex flex-col items-center justify-center p-6 backface-hidden shadow-inner">
                        <span id="fc-gender" class="text-[10px] uppercase tracking-widest text-neutral-400 bg-neutral-900 border border-neutral-800 px-3 py-1 rounded-full mb-4 font-semibold shadow">Kelime Seti</span>
                        <h2 id="fc-russian" class="text-4xl font-black text-white mb-3 text-center tracking-tight">мальчик</h2>
                        <p id="fc-pronounce" class="text-sm text-neutral-400 font-mono tracking-wider">[ mal'çik ]</p>
                    </div>
                    <!-- Back -->
                    <div class="absolute inset-0 w-full h-full bg-neutral-950 border-2 border-neutral-700 rounded-2xl flex flex-col items-center justify-center p-6 backface-hidden rotate-y-180 shadow-inner">
                        <span class="text-[10px] uppercase tracking-widest text-neutral-400 bg-neutral-900 border border-neutral-800 px-3 py-1 rounded-full mb-4 font-semibold shadow">Türkçe Anlamı</span>
                        <h2 id="fc-turkish" class="text-3xl font-black text-white text-center tracking-tight">Erkek çocuk</h2>
                    </div>
                </div>
            </div>

            <!-- Controls -->
            <div class="flex gap-4 w-full max-w-md">
                <button onclick="prevCard()" class="flex-1 bg-black hover:bg-neutral-900 border border-neutral-800 py-3 rounded-xl text-sm font-semibold transition shadow-lg flex items-center justify-center gap-2 text-neutral-200">⬅ Önceki</button>
                <button onclick="nextCard()" class="flex-1 bg-white hover:bg-neutral-200 py-3 rounded-xl text-sm font-semibold transition shadow-lg text-black">Sonraki ➡</button>
            </div>
        </section>

        <!-- MATCHING GAME SECTION -->
        <section id="section-matching" class="tab-content hidden flex flex-col gap-6">
            <div class="flex justify-between items-center bg-black p-4 rounded-xl border border-neutral-800 shadow-xl">
                <div>
                    <h3 class="font-bold text-sm text-white">Kelime Eşleştirme Bulmacası</h3>
                    <p class="text-[11px] text-neutral-400">Rusça kelimeleri doğru anlamlarıyla eşleştir.</p>
                </div>
                <div class="text-right flex items-center gap-3">
                    <span class="text-xs text-neutral-300">Skor: <strong id="match-score" class="text-white text-sm font-bold">0</strong> / 6</span>
                    <button onclick="initMatchingGame()" class="text-xs bg-neutral-900 hover:bg-neutral-800 border border-neutral-700 px-3 py-1.5 rounded-lg text-neutral-200 transition">Yenile</button>
                </div>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div class="flex flex-col gap-2.5">
                    <h4 class="text-[11px] font-bold uppercase tracking-wider text-neutral-400 px-1">Rusça Kelimeler</h4>
                    <div id="matching-russian-col" class="flex flex-col gap-2"></div>
                </div>
                <div class="flex flex-col gap-2.5">
                    <h4 class="text-[11px] font-bold uppercase tracking-wider text-neutral-400 px-1">Türkçe Anlamları</h4>
                    <div id="matching-turkish-col" class="flex flex-col gap-2"></div>
                </div>
            </div>
        </section>

        <!-- QUIZ SECTION -->
        <section id="section-quiz" class="tab-content hidden flex flex-col gap-6">
            <div id="quiz-container" class="bg-black border border-neutral-800 rounded-2xl p-6 shadow-2xl">
                <div class="flex justify-between items-center mb-6 border-b border-neutral-800 pb-4">
                    <span id="quiz-progress" class="text-xs font-semibold text-neutral-400">Soru 1 / 10</span>
                    <span id="quiz-score-badge" class="text-xs font-semibold bg-neutral-900 text-white px-3 py-1 rounded-full border border-neutral-800 shadow">Doğru: 0</span>
                </div>

                <h3 id="quiz-question" class="text-lg font-bold text-white mb-6 leading-relaxed">Rusça kelimenin Türkçe karşılığı nedir?</h3>

                <div id="quiz-options" class="grid grid-cols-1 gap-3 mb-6"></div>

                <div class="flex justify-end">
                    <button id="quiz-next-btn" onclick="nextQuizQuestion()" class="hidden bg-white hover:bg-neutral-200 text-black px-6 py-2.5 rounded-xl text-xs font-bold uppercase tracking-wider transition shadow-lg">Sonraki Soru ➡</button>
                </div>
            </div>

            <!-- Quiz Result Card -->
            <div id="quiz-result" class="hidden bg-black border border-neutral-800 rounded-2xl p-8 text-center flex flex-col items-center gap-4 shadow-2xl">
                <h3 class="text-2xl font-black text-white">Test Tamamlandı! 🎉</h3>
                <p id="quiz-final-score" class="text-sm text-neutral-300 font-medium">Skorun: 10 / 10</p>
                <button onclick="restartQuiz()" class="bg-white hover:bg-neutral-200 text-black px-6 py-2.5 rounded-xl text-xs font-bold uppercase tracking-wider transition shadow-lg">Testi Yeniden Başlat</button>
            </div>
        </section>

    </main>

    <footer class="text-center py-4 text-[11px] text-neutral-600 tracking-wide">
        Rusça Eğitim Seti &copy; 2026
    </footer>

    <!-- Application Script -->
    <script>
        const vocabularyData = [
            // Fotoğraflardaki Tüm Kelimeler, Vurgu Değişimleri ve Cümleler Dahil Edilmiştir
            { ru: "мальчик", pron: "mal'çik", tr: "Erkek çocuk", gender: "Eril (Он)" },
            { ru: "девочка", pron: "devoçka", tr: "Kız çocuk", gender: "Dişil (Она)" },
            { ru: "ребёнок", pron: "rebënok", tr: "Çocuk", gender: "Eril / Tekil" },
            { ru: "дети", pron: "deti", tr: "Çocuklar", gender: "Çoğul" },
            { ru: "человек", pron: "çelovek", tr: "İnsan", gender: "Eril" },
            { ru: "люди", pron: "lyudi", tr: "İnsanlar / Halk", gender: "Çoğul" },
            { ru: "брат", pron: "brat", tr: "Erkek kardeş", gender: "Eril (Он)" },
            { ru: "сестра", pron: "sestra", tr: "Kız kardeş", gender: "Dişil (Она)" },
            { ru: "дом ➔ дома", pron: "dom ➔ doma", tr: "Ev / Evler (Vurgu Değişimi)", gender: "Özel Kural[span_5](start_span)[span_5](end_span)" },
            { ru: "лес ➔ леса", pron: "les ➔ lesa", tr: "Orman / Ormanlar (Vurgu Değişimi)", gender: "Özel Kural[span_6](start_span)[span_6](end_span)" },
            { ru: "город ➔ города", pron: "gorod ➔ goroda", tr: "Şehir / Şehirler (Vurgu Değişimi)", gender: "Özel Kural[span_7](start_span)[span_7](end_span)" },
            { ru: "вечер ➔ вечера", pron: "veçer ➔ veçera", tr: "Akşam / Akşamlar (Vurgu Değişimi)", gender: "Özel Kural[span_8](start_span)[span_8](end_span)" },
            { ru: "поезд ➔ поезда", pron: "poyezd ➔ poyezda", tr: "Tren / Trenler (Vurgu Değişimi)", gender: "Özel Kural[span_9](start_span)[span_9](end_span)" },
            { ru: "письмо ➔ письма", pron: "pismo ➔ pisma", tr: "Mektup / Mektuplar (Nötr -o ➔ -a)", gender: "Özel Kural[span_10](start_span)[span_10](end_span)" },
            { ru: "окно ➔ окна", pron: "akno ➔ okna", tr: "Pencere / Pencereler", gender: "Özel Kural[span_11](start_span)[span_11](end_span)" },
            { ru: "место ➔ места", pron: "mesto ➔ mesta", tr: "Yer / Mekan", gender: "Özel Kural[span_12](start_span)[span_12](end_span)" },
            { ru: "поле ➔ поля", pron: "pole ➔ polya", tr: "Tarla / Saha (Nötr -e ➔ -я)", gender: "Özel Kural[span_13](start_span)[span_13](end_span)" },
            { ru: "море ➔ моря", pron: "more ➔ morya", tr: "Deniz / Denizler", gender: "Özel Kural[span_14](start_span)[span_14](end_span)" },
            { ru: "здание ➔ здания", pron: "zdaniye ➔ zdaniya", tr: "Bina / Binalar", gender: "Özel Kural[span_15](start_span)[span_15](end_span)" },
            { ru: "упражнение ➔ упражнения", pron: "uproçneniye ➔ uproçneniya", tr: "Alıştırma / Alıştırmalar", gender: "Özel Kural[span_16](start_span)[span_16](end_span)" },
            { ru: "аудитория ➔ аудитории", pron: "auditoriya ➔ auditorii", tr: "Derslik", gender: "Tablo Doldurma[span_17](start_span)[span_17](end_span)" },
            { ru: "лаборатория ➔ лаборатории", pron: "laboratoriya ➔ laboratorii", tr: "Laboratuvar", gender: "Tablo Doldurma[span_18](start_span)[span_18](end_span)" },
            { ru: "экскурсия ➔ экскурсии", pron: "eksursiya ➔ eksursii", tr: "Gezi / Konferans", gender: "Tablo Doldurma[span_19](start_span)[span_19](end_span)" },
            { ru: "станция ➔ станции", pron: "stantsiya ➔ stantsii", tr: "İstasyon", gender: "Tablo Doldurma[span_20](start_span)[span_20](end_span)" },
            { ru: "фотография ➔ фотографии", pron: "fotografiya ➔ fotografii", tr: "Fotoğraf", gender: "Tablo Doldurma[span_21](start_span)[span_21](end_span)" },
            { ru: "предложение ➔ предложения", pron: "predlojeniye ➔ predlojeniya", tr: "Cümle", gender: "Tablo Doldurma[span_22](start_span)[span_22](end_span)" },
            { ru: "общежитие ➔ общежития", pron: "obşçejitiye ➔ obşçejitiya", tr: "Yurt", gender: "Tablo Doldurma[span_23](start_span)[span_23](end_span)" },
            { ru: "Это карандаш ➔ Это карандаши", pron: "eta karandaş ➔ eta karandaşi", tr: "Bu bir kurşun kalem ➔ Bunlar kurşun kalemdir", gender: "Cümle Dönüşümü[span_24](start_span)[span_24](end_span)[span_25](start_span)[span_25](end_span)" },
            { ru: "Это лампа ➔ Это лампы", pron: "eta lampa ➔ eta lampi", tr: "Bu bir lamba ➔ Bunlar lambadır", gender: "Cümle Dönüşümü[span_26](start_span)[span_26](end_span)[span_27](start_span)[span_27](end_span)" },
            { ru: "Это дом ➔ Это дома", pron: "eta dom ➔ eta doma", tr: "Bu bir ev ➔ Bunlar evler", gender: "Cümle Dönüşümü[span_28](start_span)[span_28](end_span)[span_29](start_span)[span_29](end_span)" },
            { ru: "Это письмо ➔ Это письма", pron: "eta pismo ➔ eta pisma", tr: "Bu bir mektup ➔ Bunlar mektuplar", gender: "Cümle Dönüşümü[span_30](start_span)[span_30](end_span)[span_31](start_span)[span_31](end_span)" },
            { ru: "Учительница", pron: "Uçitel'nitsa", tr: "Kadın öğretmen", gender: "Dişil (Feminine)" },
            { ru: "Ученица", pron: "Uçenitsa", tr: "Kız öğrenci", gender: "Dişil (Feminine)" },
            { ru: "Учитель", pron: "Uçitel'", tr: "Erkek öğretmen", gender: "Eril (Masculine)" },
            { ru: "Семья", pron: "Sem'ya", tr: "Aile", gender: "Dişil" },
            { ru: "Понедельник", pron: "Panedel'nik", tr: "Pazartesi", gender: "Eril" },
            { ru: "Вторник", pron: "Vtornik", tr: "Salı (Ftornik okunur)", gender: "Eril" },
            { ru: "Среда", pron: "Sreda", tr: "Çarşamba", gender: "Dişil" },
            { ru: "Четверг", pron: "Çetverk", tr: "Perşembe", gender: "Eril" },
            { ru: "Пятница", pron: "Pyatnitsa", tr: "Cuma", gender: "Dişil" },
            { ru: "Суббота", pron: "Subbota", tr: "Cumartesi", gender: "Dişil" },
            { ru: "Воскресенье", pron: "Vaskresen'ye", tr: "Pazar", gender: "Nötr" },
            { ru: "Пальто", pron: "Pal'to", tr: "Palto", gender: "İndeklinabl (Değişmez)" },
            { ru: "Метро", pron: "Metra", tr: "Metro", gender: "İndeklinabl (Değişmez)" },
            { ru: "Кафе", pron: "Kafe", tr: "Kafe", gender: "İndeklinabl (Değişmez)" },
            { ru: "Ножницы", pron: "Nojnitsı", tr: "Makas", gender: "Sadece Çoğul (Pluralia Tantum)" },
            { ru: "Очки", pron: "Oçki", tr: "Gözlük", gender: "Sadece Çoğul (Pluralia Tantum)" },
            { ru: "Деньги", pron: "Dengi", tr: "Para", gender: "Sadece Çoğul (Pluralia Tantum)" }
        ];

        // Gramer Notları Paneli Açma/Kapatma Fonksiyonu
        function toggleNotes() {
            const panel = document.getElementById('notesPanel');
            panel.classList.toggle('hidden');
        }

        // Tab Switcher
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById('section-' + tabId).classList.remove('hidden');

            ['flashcards', 'matching', 'quiz'].forEach(t => {
                const btn = document.getElementById('btn-' + t);
                if (t === tabId) {
                    btn.className = "px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all bg-white text-black shadow-lg";
                } else {
                    btn.className = "px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all text-neutral-400 hover:text-white hover:bg-neutral-900";
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
                btn.className = "w-full p-3 bg-black hover:bg-neutral-900 border border-neutral-800 rounded-xl text-left text-xs font-medium transition flex justify-between items-center text-neutral-100 shadow";
                btn.innerHTML = `<span>${item.ru}</span> <span class="text-[10px] text-neutral-500 font-mono">[${item.pron}]</span>`;
                btn.onclick = () => selectRussian(item, btn);
                ruCol.appendChild(btn);
            });

            trShuffled.forEach(item => {
                const btn = document.createElement('button');
                btn.className = "w-full p-3 bg-black hover:bg-neutral-900 border border-neutral-800 rounded-xl text-left text-xs font-medium transition text-neutral-100 shadow";
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
            if (btn.classList.contains('bg-neutral-900') && btn.classList.contains('opacity-40')) return;
            if (activeRuBtn) activeRuBtn.classList.remove('border-white', 'bg-neutral-900');
            activeRuBtn = btn;
            currentRuItem = item;
            btn.classList.add('border-white', 'bg-neutral-900');
            checkMatch();
        }

        function selectTurkish(item, btn) {
            if (btn.classList.contains('bg-neutral-900') && btn.classList.contains('opacity-40')) return;
            if (activeTrBtn) activeTrBtn.classList.remove('border-white', 'bg-neutral-900');
            activeTrBtn = btn;
            currentTrItem = item;
            btn.classList.add('border-white', 'bg-neutral-900');
            checkMatch();
        }

        function checkMatch() {
            if (currentRuItem && currentTrItem) {
                if (currentRuItem.ru === currentTrItem.ru) {
                    activeRuBtn.className = "w-full p-3 bg-neutral-950 border border-neutral-800 rounded-xl text-left text-xs font-medium text-neutral-500 opacity-40 cursor-default flex justify-between items-center shadow-inner";
                    activeTrBtn.className = "w-full p-3 bg-neutral-950 border border-neutral-800 rounded-xl text-left text-xs font-medium text-neutral-500 opacity-40 cursor-default shadow-inner";
                    matchedCount++;
                    document.getElementById('match-score').innerText = matchedCount;

                    if (matchedCount === 6) {
                        setTimeout(() => {
                            alert("Tebrikler kanka! Tüm eşleştirmeleri bitirdin! 🎉");
                            initMatchingGame();
                        }, 300);
                    }
                } else {
                    activeRuBtn.classList.remove('border-white', 'bg-neutral-900');
                    activeTrBtn.classList.remove('border-white', 'bg-neutral-900');
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
            document.getElementById('quiz-question').innerHTML = `"<span class="text-white font-bold">${q.ru}</span>" <span class="text-xs text-neutral-500 font-mono">([${q.pron}] - ${q.gender})</span> kelimesinin Türkçe karşılığı nedir?`;
            
            const optionsContainer = document.getElementById('quiz-options');
            optionsContainer.innerHTML = '';

            q.options.forEach(opt => {
                const btn = document.createElement('button');
                btn.className = "w-full p-3.5 bg-black hover:bg-neutral-900 border border-neutral-800 rounded-xl text-xs font-medium text-left transition text-neutral-100 shadow";
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
                    b.className = "w-full p-3.5 bg-neutral-900 border border-white rounded-xl text-xs font-medium text-left text-white shadow";
                } else if (b === btn && selected !== correct) {
                    b.className = "w-full p-3.5 bg-neutral-950 border border-neutral-700 rounded-xl text-xs font-medium text-left text-neutral-500 shadow";
                } else {
                    b.className = "w-full p-3.5 bg-black border border-neutral-900 rounded-xl text-xs font-medium text-left text-neutral-600 shadow";
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

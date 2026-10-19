<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rusça Öğrenme Merkezi</title>
    <script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>
    <style>
        .perspective-1000 { perspective: 1000px; }
        .transform-style-3d { transform-style: preserve-3d; }
        .backface-hidden { backface-visibility: hidden; }
        .rotate-y-180 { transform: rotateY(180deg); }
        body {
            background-color: #0c1a17;
            background-image: radial-gradient(circle at 50% 0%, #132e29 0%, #0c1a17 100%);
        }
    </style>
</head>
<body class="text-emerald-100 min-h-screen flex flex-col font-sans selection:bg-emerald-500 selection:text-white">
    
    <!-- Header / Navbar -->
    <header class="w-full max-w-4xl mx-auto p-4 sm:p-6">
        <div class="bg-[#102521] border border-[#1b3d36] shadow-2xl rounded-2xl py-4 px-6 flex flex-col sm:flex-row justify-between items-center gap-4 backdrop-blur-md">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-emerald-400 to-teal-700 flex items-center justify-center shadow-lg font-bold text-slate-900 text-lg">RU</div>
                <div>
                    <h1 class="text-base font-bold text-white tracking-wide">Rusça Çalışma Alanı</h1>
                    <p class="text-[11px] text-emerald-400/80">İnteraktif Eğitim Portalı</p>
                </div>
            </div>
            
            <!-- Navigation Tabs -->
            <nav class="flex gap-2 bg-[#0c1a17] p-1.5 rounded-xl border border-[#183630]">
                <button onclick="switchTab('flashcards')" id="btn-flashcards" class="px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all bg-emerald-600 text-white shadow-lg shadow-emerald-900/40">Flashcards</button>
                <button onclick="switchTab('matching')" id="btn-matching" class="px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all text-emerald-300/70 hover:text-white hover:bg-[#132e29]">Eşleştirme</button>
                <button onclick="switchTab('quiz')" id="btn-quiz" class="px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all text-emerald-300/70 hover:text-white hover:bg-[#132e29]">Test</button>
            </nav>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-4xl w-full mx-auto p-4 sm:p-6 flex flex-col justify-center">

        <!-- FLASHCARDS SECTION -->
        <section id="section-flashcards" class="tab-content flex flex-col items-center gap-6">
            <div class="w-full flex justify-between items-center text-xs text-emerald-400/80 px-2 font-medium">
                <span id="fc-progress" class="bg-[#102521] border border-[#1b3d36] px-3 py-1.5 rounded-lg shadow">Kart 1 / 150</span>
                <span class="bg-[#102521] border border-[#1b3d36] px-3 py-1.5 rounded-lg shadow">Çevirmek için karta tıkla</span>
            </div>

            <!-- Card Element -->
            <div class="w-full max-w-md h-72 perspective-1000 cursor-pointer group" onclick="flipCard()">
                <div id="flashcard-inner" class="relative w-full h-full duration-500 transform-style-3d shadow-2xl rounded-2xl">
                    <!-- Front -->
                    <div class="absolute inset-0 w-full h-full bg-gradient-to-br from-[#132e29] to-[#0f2420] border-2 border-[#1f4840] rounded-2xl flex flex-col items-center justify-center p-6 backface-hidden shadow-inner">
                        <span id="fc-gender" class="text-[10px] uppercase tracking-widest text-emerald-400 bg-emerald-950/80 border border-emerald-800/50 px-3 py-1 rounded-full mb-4 font-semibold shadow">Kelime Seti</span>
                        <h2 id="fc-russian" class="text-4xl font-black text-white mb-3 text-center tracking-tight">мальчик</h2>
                        <p id="fc-pronounce" class="text-sm text-emerald-300/70 font-mono tracking-wider">[ mal'çik ]</p>
                    </div>
                    <!-- Back -->
                    <div class="absolute inset-0 w-full h-full bg-gradient-to-br from-[#0f2420] to-[#132e29] border-2 border-teal-800/60 rounded-2xl flex flex-col items-center justify-center p-6 backface-hidden rotate-y-180 shadow-inner">
                        <span class="text-[10px] uppercase tracking-widest text-teal-400 bg-teal-950/80 border border-teal-800/50 px-3 py-1 rounded-full mb-4 font-semibold shadow">Türkçe Anlamı</span>
                        <h2 id="fc-turkish" class="text-3xl font-black text-white text-center tracking-tight">Erkek çocuk</h2>
                    </div>
                </div>
            </div>

            <!-- Controls -->
            <div class="flex gap-4 w-full max-w-md">
                <button onclick="prevCard()" class="flex-1 bg-[#102521] hover:bg-[#16352f] border border-[#1b3d36] py-3 rounded-xl text-sm font-semibold transition shadow-lg flex items-center justify-center gap-2 text-emerald-200">⬅ Önceki</button>
                <button onclick="nextCard()" class="flex-1 bg-emerald-600 hover:bg-emerald-500 py-3 rounded-xl text-sm font-semibold transition shadow-lg shadow-emerald-900/40 flex items-center justify-center gap-2 text-white">Sonraki ➡</button>
            </div>
        </section>

        <!-- MATCHING GAME SECTION -->
        <section id="section-matching" class="tab-content hidden flex flex-col gap-6">
            <div class="flex justify-between items-center bg-[#102521] p-4 rounded-xl border border-[#1b3d36] shadow-xl">
                <div>
                    <h3 class="font-bold text-sm text-white">Kelime Eşleştirme Bulmacası</h3>
                    <p class="text-[11px] text-emerald-400/70">Rusça kelimeleri doğru anlamlarıyla eşleştir.</p>
                </div>
                <div class="text-right flex items-center gap-3">
                    <span class="text-xs text-emerald-300">Skor: <strong id="match-score" class="text-emerald-400 text-sm font-bold">0</strong> / 6</span>
                    <button onclick="initMatchingGame()" class="text-xs bg-[#16352f] hover:bg-[#1f4840] border border-[#235248] px-3 py-1.5 rounded-lg text-emerald-200 transition">Yenile</button>
                </div>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div class="flex flex-col gap-2.5">
                    <h4 class="text-[11px] font-bold uppercase tracking-wider text-emerald-400 px-1">Rusça Kelimeler</h4>
                    <div id="matching-russian-col" class="flex flex-col gap-2"></div>
                </div>
                <div class="flex flex-col gap-2.5">
                    <h4 class="text-[11px] font-bold uppercase tracking-wider text-teal-400 px-1">Türkçe Anlamları</h4>
                    <div id="matching-turkish-col" class="flex flex-col gap-2"></div>
                </div>
            </div>
        </section>

        <!-- QUIZ SECTION -->
        <section id="section-quiz" class="tab-content hidden flex flex-col gap-6">
            <div id="quiz-container" class="bg-[#102521] border border-[#1b3d36] rounded-2xl p-6 shadow-2xl">
                <div class="flex justify-between items-center mb-6 border-b border-[#1b3d36] pb-4">
                    <span id="quiz-progress" class="text-xs font-semibold text-emerald-400/80">Soru 1 / 10</span>
                    <span id="quiz-score-badge" class="text-xs font-semibold bg-emerald-950 text-emerald-300 px-3 py-1 rounded-full border border-emerald-800/60 shadow">Doğru: 0</span>
                </div>

                <h3 id="quiz-question" class="text-lg font-bold text-white mb-6 leading-relaxed">Rusça kelimenin Türkçe karşılığı nedir?</h3>

                <div id="quiz-options" class="grid grid-cols-1 gap-3 mb-6"></div>

                <div class="flex justify-end">
                    <button id="quiz-next-btn" onclick="nextQuizQuestion()" class="hidden bg-emerald-600 hover:bg-emerald-500 text-white px-6 py-2.5 rounded-xl text-xs font-bold uppercase tracking-wider transition shadow-lg shadow-emerald-900/40">Sonraki Soru ➡</button>
                </div>
            </div>

            <!-- Quiz Result Card -->
            <div id="quiz-result" class="hidden bg-[#102521] border border-[#1b3d36] rounded-2xl p-8 text-center flex flex-col items-center gap-4 shadow-2xl">
                <h3 class="text-2xl font-black text-white">Test Tamamlandı! 🎉</h3>
                <p id="quiz-final-score" class="text-sm text-emerald-300 font-medium">Skorun: 10 / 10</p>
                <button onclick="restartQuiz()" class="bg-emerald-600 hover:bg-emerald-500 text-white px-6 py-2.5 rounded-xl text-xs font-bold uppercase tracking-wider transition shadow-lg shadow-emerald-900/40">Testi Yeniden Başlat</button>
            </div>
        </section>

    </main>

    <footer class="text-center py-4 text-[11px] text-emerald-500/50 tracking-wide">
        Rusça Eğitim Seti &copy; 2026
    </footer>

    <!-- Application Script -->
    <script>
        const vocabularyData = [
            // PDF 1 & PDF 2 Birleştirilmiş Kelime Listesi
            { ru: "мальчик", pron: "mal'çik", tr: "Erkek çocuk", gender: "Eril (Он)" },
            { ru: "девочка", pron: "devoçka", tr: "Kız çocuk", gender: "Dişil (Она)" },
            { ru: "ребёнок", pron: "rebënok", tr: "Çocuk", gender: "Eril / Tekil" },
            { ru: "дети", pron: "deti", tr: "Çocuklar", gender: "Çoğul" },
            { ru: "человек", pron: "çelovek", tr: "İnsan", gender: "Eril" },
            { ru: "люди", pron: "lyudi", tr: "İnsanlar / Halk", gender: "Çoğul" },
            { ru: "брат", pron: "brat", tr: "Erkek kardeş", gender: "Eril (Он)" },
            { ru: "сестра", pron: "sestra", tr: "Kız kardeş", gender: "Dişil (Она)" },
            { ru: "отец", pron: "otets", tr: "Baba", gender: "Eril (Он)" },
            { ru: "мать", pron: "mat'", tr: "Anne", gender: "Dişil (Она)" },
            { ru: "дочь", pron: "doç'", tr: "Kız evlat", gender: "Dişil (Она)" },
            { ru: "сын", pron: "sin", tr: "Oğul / Erkek evlat", gender: "Eril (Он)" },
            { ru: "друг", pron: "drug", tr: "Arkadaş / Dost", gender: "Eril (Он)" },
            { ru: "студент", pron: "student", tr: "Erkek üniversite öğrencisi", gender: "Eril (Он)" },
            { ru: "студентка", pron: "studentka", tr: "Kız üniversite öğrencisi", gender: "Dişil (Она)" },
            { ru: "врач", pron: "vraç", tr: "Doktor", gender: "Eril (Он)" },
            { ru: "инженер", pron: "injener", tr: "Mühendis", gender: "Eril (Он)" },
            { ru: "дом", pron: "dom", tr: "Ev / Bina", gender: "Eril (Он)" },
            { ru: "улица", pron: "ulitsa", tr: "Cadde / Sokak", gender: "Dişil (Она)" },
            { ru: "город", pron: "gorod", tr: "Şehir", gender: "Eril (Он)" },
            { ru: "деревня", pron: "derevnya", tr: "Köy", gender: "Dişil (Она)" },
            { ru: "школа", pron: "şkola", tr: "Okul", gender: "Dişil (Она)" },
            { ru: "университет", pron: "universitet", tr: "Üniversite", gender: "Eril (Он)" },
            { ru: "общежитие", pron: "obşçejitiye", tr: "Öğrenci yurdu", gender: "Nötr (Оно)" },
            { ru: "магазин", pron: "magazin", tr: "Mağaza / Dükkan", gender: "Eril (Он)" },
            { ru: "парк", pron: "park", tr: "Park", gender: "Eril (Он)" },
            { ru: "сад", pron: "sad", tr: "Bahçe", gender: "Eril (Он)" },
            { ru: "автобус", pron: "avtobus", tr: "Otobüs", gender: "Eril (Он)" },
            { ru: "трамвай", pron: "tramvay", tr: "Tramvay", gender: "Eril (Он)" },
            { ru: "машина", pron: "maşina", tr: "Araba", gender: "Dişil (Она)" },
            { ru: "поезд", pron: "poyezd", tr: "Tren", gender: "Eril (Он)" },
            { ru: "стол", pron: "stol", tr: "Masa", gender: "Eril (Он)" },
            { ru: "стул", pron: "stul", tr: "Sandalye", gender: "Eril (Он)" },
            { ru: "шкаф", pron: "şkaf", tr: "Dolap / Gardırop", gender: "Eril (Он)" },
            { ru: "кресло", pron: "kreslo", tr: "Tekli koltuk / Berjer", gender: "Nötr (Оно)" },
            { ru: "окно", pron: "okno", tr: "Pencere", gender: "Nötr (Оно)" },
            { ru: "дверь", pron: "dver'", tr: "Kapı", gender: "Dişil (Она)" },
            { ru: "книга", pron: "kniga", tr: "Kitap", gender: "Dişil (Она)" },
            { ru: "тетрадь", pron: "tetrad'", tr: "Defter", gender: "Dişil (Она)" },
            { ru: "учебник", pron: "uçebnik", tr: "Ders kitabı", gender: "Eril (Он)" },
            { ru: "журнал", pron: "jurnal", tr: "Dergi", gender: "Eril (Он)" },
            { ru: "газета", pron: "gazeta", tr: "Gazete", gender: "Dişil (Она)" },
            { ru: "ручка", pron: "ruçka", tr: "Kalem (Tükenmez)", gender: "Dişil (Она)" },
            { ru: "карандаш", pron: "karandaş", tr: "Kurşun kalem", gender: "Eril (Он)" },
            { ru: "письмо", pron: "pis'mo", tr: "Mektup", gender: "Nötr (Оно)" },
            { ru: "словарь", pron: "slovar'", tr: "Sözlük", gender: "Eril (Он)" },
            { ru: "телевизор", pron: "televizor", tr: "Televizyon", gender: "Eril (Он)" },
            { ru: "костюм", pron: "kostyum", tr: "Takım elbise", gender: "Eril (Он)" },
            { ru: "портфель", pron: "portfel'", tr: "Çanta / Evrak çantası", gender: "Eril (Он)" },
            { ru: "фотография", pron: "fotografiya", tr: "Fotoğraf", gender: "Dişil (Она)" },
            { ru: "фильм", pron: "fil'm", tr: "Film", gender: "Eril (Он)" },
            { ru: "урок", pron: "urok", tr: "Ders", gender: "Eril (Он)" },
            { ru: "текст", pron: "tekst", tr: "Metin", gender: "Eril (Он)" },
            { ru: "роман", pron: "roman", tr: "Roman", gender: "Eril (Он)" },
            { ru: "слово", pron: "slovo", tr: "Kelime", gender: "Nötr (Оно)" },
            { ru: "буква", pron: "bukva", tr: "Harf", gender: "Dişil (Она)" },
            { ru: "правило", pron: "pravilo", tr: "Kural", gender: "Nötr (Оно)" },
            { ru: "вопрос", pron: "vopros", tr: "Soru", gender: "Eril (Он)" },
            { ru: "ответ", pron: "otvet", tr: "Cevap / Yanıt", gender: "Eril (Он)" },
            { ru: "ошибка", pron: "oşibka", tr: "Hata / Yanlış", gender: "Dişil (Она)" },
            { ru: "класс", pron: "klass", tr: "Sınıf / Derslik", gender: "Eril (Он)" },
            { ru: "язык", pron: "yazık", tr: "Dil", gender: "Eril (Он)" },
            { ru: "шахматы", pron: "şahmatı", tr: "Satranç", gender: "Çoğul" },
            { ru: "футбол", pron: "futbol", tr: "Futbol", gender: "Eril (Он)" },
            { ru: "теннис", pron: "tennis", tr: "Tenis", gender: "Eril (Он)" },
            { ru: "читать", pron: "çitat'", tr: "Okumak", gender: "Fiil" },
            { ru: "писать", pron: "pisat'", tr: "Yazmak", gender: "Fiil" },
            { ru: "работать", pron: "rabotat'", tr: "Çalışmak", gender: "Fiil" },
            { ru: "отдыхать", pron: "otdıhat'", tr: "Dinlenmek", gender: "Fiil" },
            { ru: "знать", pron: "znat'", tr: "Bilmek", gender: "Fiil" },
            { ru: "слушать", pron: "sluşat'", tr: "Dinlemek", gender: "Fiil" },
            { ru: "понимать", pron: "ponimat'", tr: "Anlamak", gender: "Fiil" },
            { ru: "говорить", pron: "govorit'", tr: "Konuşmak", gender: "Fiil" },
            { ru: "смотреть", pron: "smotret'", tr: "İzlemek / Bakmak", gender: "Fiil" },
            { ru: "играть", pron: "igrat'", tr: "Oynamak", gender: "Fiil" },
            { ru: "думать", pron: "dumat'", tr: "Düşünmek", gender: "Fiil" },
            { ru: "хорошо", pron: "horoşo", tr: "İyi / Güzel", gender: "Zarf" },
            { ru: "плохо", pron: "ploho", tr: "Kötü", gender: "Zarf" },
            { ru: "быстро", pron: "bistro", tr: "Hızlı", gender: "Zarf" },
            { ru: "медленно", pron: "medlenno", tr: "Yavaş", gender: "Zarf" },
            { ru: "сегодня", pron: "segodnya", tr: "Bugün", gender: "Zaman" },
            { ru: "вчера", pron: "vçera", tr: "Dün", gender: "Zaman" },
            { ru: "завтра", pron: "zavtra", tr: "Yarın", gender: "Zaman" },
            { ru: "спутник", pron: "sputnik", tr: "Uydu", gender: "Eril (Он)" },
            { ru: "нож", pron: "noj", tr: "Bıçak", gender: "Eril (Он)" },
            { ru: "мяч", pron: "myaç", tr: "Top", gender: "Eril (Он)" },
            { ru: "хлеб", pron: "hleb", tr: "Ekmek", gender: "Eril (Он)" },
            { ru: "остров", pron: "ostrov", tr: "Ada", gender: "Eril (Он)" },
            { ru: "музей", pron: "muzey", tr: "Müze", gender: "Eril (Он)" },
            { ru: "чай", pron: "çay", tr: "Çay", gender: "Eril (Он)" },
            { ru: "вокзал", pron: "vokzal", tr: "Tren garı", gender: "Eril (Он)" },
            { ru: "семья", pron: "sem'ya", tr: "Aile", gender: "Dişil (Она)" },
            { ru: "рыба", pron: "ryba", tr: "Balık", gender: "Dişil (Она)" },
            { ru: "звезда", pron: "zvezda", tr: "Yıldız", gender: "Dişil (Она)" },
            { ru: "кухня", pron: "kuhnya", tr: "Mutfak", gender: "Dişil (Она)" },
            { ru: "вода", pron: "voda", tr: "Su", gender: "Dişil (Она)" },
            { ru: "страна", pron: "strana", tr: "Ülke", gender: "Dişil (Она)" },
            { ru: "платье", pron: "plat'ye", tr: "Elbise", gender: "Nötr (Оно)" },
            { ru: "кольцо", pron: "kol'tso", tr: "Yüzük", gender: "Nötr (Оно)" },
            { ru: "дерево", pron: "derevo", tr: "Ağaç", gender: "Nötr (Оно)" },
            { ru: "яблоко", pron: "yabloko", tr: "Elma", gender: "Nötr (Оно)" },
            { ru: "солнце", pron: "solntse", tr: "Güneş", gender: "Nötr (Оно)" },
            { ru: "море", pron: "more", tr: "Deniz", gender: "Nötr (Оно)" },
            { ru: "время", pron: "vremya", tr: "Zaman", gender: "Nötr (-мя)" },
            { ru: "имя", pron: "imya", tr: "Ad / İsim", gender: "Nötr (-мя)" },
            { ru: "дождь", pron: "dojd'", tr: "Yağmur", gender: "Eril (Он)" },
            { ru: "день", pron: "den'", tr: "Gün", gender: "Eril (Он)" },
            { ru: "ночь", pron: "noç'", tr: "Gece", gender: "Dişil (Она)" },
            { ru: "любовь", pron: "lyubov'", tr: "Aşk / Sevgi", gender: "Dişil (Она)" },
            { ru: "папа", pron: "papa", tr: "Baba", gender: "Eril (İstisna)" },
            { ru: "дедушка", pron: "deduşka", tr: "Dede", gender: "Eril (İstisna)" },
            { ru: "пальто", pron: "pal'to", tr: "Palto", gender: "Nötr (Değişmez)" },
            { ru: "кино", pron: "kino", tr: "Sinema", gender: "Nötr (Değişmez)" }
        ];

        // Tab Switcher
        function switchTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.getElementById('section-' + tabId).classList.remove('hidden');

            ['flashcards', 'matching', 'quiz'].forEach(t => {
                const btn = document.getElementById('btn-' + t);
                if (t === tabId) {
                    btn.className = "px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all bg-emerald-600 text-white shadow-lg shadow-emerald-900/40";
                } else {
                    btn.className = "px-4 py-2 rounded-lg text-xs font-semibold tracking-wider uppercase transition-all text-emerald-300/70 hover:text-white hover:bg-[#132e29]";
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
                btn.className = "w-full p-3 bg-[#132e29] hover:bg-[#193c36] border border-[#1f4840] rounded-xl text-left text-xs font-medium transition flex justify-between items-center text-emerald-100 shadow";
                btn.innerHTML = `<span>${item.ru}</span> <span class="text-[10px] text-emerald-400/70 font-mono">[${item.pron}]</span>`;
                btn.onclick = () => selectRussian(item, btn);
                ruCol.appendChild(btn);
            });

            trShuffled.forEach(item => {
                const btn = document.createElement('button');
                btn.className = "w-full p-3 bg-[#132e29] hover:bg-[#193c36] border border-[#1f4840] rounded-xl text-left text-xs font-medium transition text-emerald-100 shadow";
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
            if (btn.classList.contains('bg-emerald-950')) return;
            if (activeRuBtn) activeRuBtn.classList.remove('border-emerald-400', 'bg-[#1c443d]');
            activeRuBtn = btn;
            currentRuItem = item;
            btn.classList.add('border-emerald-400', 'bg-[#1c443d]');
            checkMatch();
        }

        function selectTurkish(item, btn) {
            if (btn.classList.contains('bg-emerald-950')) return;
            if (activeTrBtn) activeTrBtn.classList.remove('border-teal-400', 'bg-[#1c443d]');
            activeTrBtn = btn;
            currentTrItem = item;
            btn.classList.add('border-teal-400', 'bg-[#1c443d]');
            checkMatch();
        }

        function checkMatch() {
            if (currentRuItem && currentTrItem) {
                if (currentRuItem.ru === currentTrItem.ru) {
                    activeRuBtn.className = "w-full p-3 bg-emerald-950/60 border border-emerald-600 rounded-xl text-left text-xs font-medium text-emerald-300 opacity-60 cursor-default flex justify-between items-center shadow-inner";
                    activeTrBtn.className = "w-full p-3 bg-emerald-950/60 border border-emerald-600 rounded-xl text-left text-xs font-medium text-emerald-300 opacity-60 cursor-default shadow-inner";
                    matchedCount++;
                    document.getElementById('match-score').innerText = matchedCount;

                    if (matchedCount === 6) {
                        setTimeout(() => {
                            alert("Tebrikler! Tüm kelimeleri başarıyla eşleştirdin! 🎉");
                            initMatchingGame();
                        }, 300);
                    }
                } else {
                    activeRuBtn.classList.remove('border-emerald-400', 'bg-[#1c443d]');
                    activeTrBtn.classList.remove('border-teal-400', 'bg-[#1c443d]');
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
            document.getElementById('quiz-question').innerHTML = `"<span class="text-emerald-400 font-bold">${q.ru}</span>" <span class="text-xs text-emerald-300/60 font-mono">([${q.pron}] - ${q.gender})</span> kelimesinin Türkçe karşılığı nedir?`;
            
            const optionsContainer = document.getElementById('quiz-options');
            optionsContainer.innerHTML = '';

            q.options.forEach(opt => {
                const btn = document.createElement('button');
                btn.className = "w-full p-3.5 bg-[#132e29] hover:bg-[#193c36] border border-[#1f4840] rounded-xl text-xs font-medium text-left transition text-emerald-100 shadow";
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
                    b.className = "w-full p-3.5 bg-emerald-900/60 border border-emerald-500 rounded-xl text-xs font-medium text-left text-white shadow";
                } else if (b === btn && selected !== correct) {
                    b.className = "w-full p-3.5 bg-rose-950/60 border border-rose-600 rounded-xl text-xs font-medium text-left text-white shadow";
                } else {
                    b.className = "w-full p-3.5 bg-[#102521] border border-[#183630] rounded-xl text-xs font-medium text-left text-emerald-500/50 shadow";
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

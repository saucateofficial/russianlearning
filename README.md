<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rusça Kapsamlı Kelime ve Gramer Defterim</title>
    <style>
        :root {
            --bg-color: #ffffff;
            --text-color: #111111;
            --border-color: #111111;
            --card-bg: #f9f9f9;
            --hover-bg: #111111;
            --hover-text: #ffffff;
        }

        body {
            font-family: 'Courier New', Courier, monospace;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }

        header {
            text-align: center;
            border-bottom: 3px solid var(--border-color);
            padding-bottom: 20px;
            margin-bottom: 30px;
            position: relative;
        }

        h1 {
            font-size: 2.3rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            margin: 0;
        }

        p.subtitle {
            font-style: italic;
            margin-top: 5px;
        }

        /* Not Kutusu (Açılıp Kapanabilir) */
        .notes-container {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1000;
        }

        .notes-toggle-btn {
            background: var(--text-color);
            color: var(--bg-color);
            border: 2px solid var(--border-color);
            padding: 10px 15px;
            font-family: inherit;
            font-weight: bold;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 3px 3px 0px #000;
        }

        .notes-toggle-btn:active {
            transform: translate(2px, 2px);
            box-shadow: 1px 1px 0px #000;
        }

        .notes-content {
            display: none;
            position: absolute;
            right: 0;
            top: 45px;
            width: 360px;
            max-height: 480px;
            overflow-y: auto;
            background: var(--bg-color);
            border: 2px solid var(--border-color);
            padding: 15px;
            box-shadow: 5px 5px 0px #000;
            font-size: 0.8rem;
        }

        .notes-content.active {
            display: block;
        }

        .notes-content h3 {
            margin-top: 0;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 5px;
            font-size: 0.95rem;
        }

        .notes-content ul {
            padding-left: 15px;
            margin-bottom: 0;
        }

        .notes-content li {
            margin-bottom: 8px;
        }

        /* Arama Çubuğu */
        .search-box {
            text-align: center;
            margin-bottom: 30px;
        }

        .search-box input {
            width: 60%;
            max-width: 400px;
            padding: 10px;
            font-family: inherit;
            border: 2px solid var(--border-color);
            font-size: 1rem;
            outline: none;
        }

        /* Liste Düzeni */
        .category-section {
            margin-bottom: 40px;
            border: 2px solid var(--border-color);
            padding: 20px;
            background: var(--card-bg);
            box-shadow: 4px 4px 0px #000;
        }

        .category-section h2 {
            border-bottom: 2px solid var(--border-color);
            padding-bottom: 10px;
            margin-top: 0;
            text-transform: uppercase;
            font-size: 1.2rem;
            letter-spacing: 1px;
        }

        .word-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 15px;
        }

        .word-card {
            background: var(--bg-color);
            border: 1px solid var(--border-color);
            padding: 12px;
            transition: 0.2s;
        }

        .word-card:hover {
            background: var(--hover-bg);
            color: var(--hover-text);
        }

        .ru {
            font-weight: bold;
            font-size: 1.05rem;
        }

        .pron {
            font-style: italic;
            opacity: 0.8;
            font-size: 0.85rem;
        }

        .tr {
            margin-top: 4px;
            font-weight: bold;
        }

        .details {
            font-size: 0.75rem;
            margin-top: 6px;
            border-top: 1px dashed currentColor;
            padding-top: 4px;
            opacity: 0.9;
        }

        footer {
            text-align: center;
            margin-top: 50px;
            border-top: 2px solid var(--border-color);
            padding-top: 20px;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>

    <!-- Not Kutusu Butonu ve Paneli -->
    <div class="notes-container">
        <button class="notes-toggle-btn" onclick="toggleNotes()">📌 Gramer Notları</button>
        <div class="notes-content" id="notesPanel">
            <h3>Temel Kurallar & İpuçları</h3>
            <ul>
                <li><strong>Cinsiyetler:</strong> Eril sessiz harfle veya -й ile biter[span_0](start_span)[span_0](end_span); dişil genellikle -а/-я ile biter[span_1](start_span)[span_1](end_span); nötr -о/-е ile biter[span_2](start_span)[span_2](end_span). -мя ile bitenler nötr istisnadır (время, имя vb.)[span_3](start_span)[span_3](end_span).</li>
                <li><strong>7 Harf İmla Kuralı:</strong> Г, К, Х, Ж, Ш, Ч, Щ harflerinden sonra asla -ы yazılmaz, mutlaka -и yazılır[span_4](start_span)[span_4](end_span).</li>
                <li><strong>Vurgu Değişimi:</strong> Bazı kelimeler çoğul yapılırken vurgu son heceye veya -а/-я ekine kayar (дом ➔ дома)[span_5](start_span)[span_5](end_span).</li>
                <li><strong>Pluralia Tantum (Sadece Çoğul):</strong> ножницы, очки, деньги, сутки, каникулы gibi kelimelerin tekil hali yoktur[span_6](start_span)[span_6](end_span).</li>
                <li><strong>İndeklinabl (Değişmeyenler):</strong> пальто, кино, метро, кафе gibi yabancı kökenli nötr kelimeler hiç ek almaz[span_7](start_span)[span_7](end_span).</li>
            </ul>
        </div>
    </div>

    <header>
        <h1>Rusça Kapsamlı Kelime Defterim</h1>
        <p class="subtitle">Tüm PDF ve defter notları, cinsiyetler, çoğullar ve kurallarla güncellendi!</p>
    </header>

    <div class="search-box">
        <input type="text" id="searchInput" placeholder="Kelime veya anlam ara..." onkeyup="searchWords()">
    </div>

    <main id="contentArea">
        <!-- 1. KISIM: İNSANLAR VE KİŞİLER -->
        <section class="category-section">
            <h2>1. İnsanlar, Kişiler ve Meslekler</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">мальчик</div>
                    <div class="pron">(mal'çik)</div>
                    <div class="tr">= Erkek çocuk</div>
                    <div class="details">Eril (Он)[span_8](start_span)[span_8](end_span) | Çoğul: мальчики[span_9](start_span)[span_9](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">девочка</div>
                    <div class="pron">(devoçka)</div>
                    <div class="tr">= Kız çocuk</div>
                    <div class="details">Dişil (Она)[span_10](start_span)[span_10](end_span) | Çoğul: девочки[span_11](start_span)[span_11](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">ребёнок ➔ дети</div>
                    <div class="pron">(rebyonok ➔ deti)</div>
                    <div class="tr">= Çocuk / Çocuklar</div>
                    <div class="details">Kökten değişen düzensiz çoğul[span_12](start_span)[span_12](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">человек ➔ люди</div>
                    <div class="pron">(çelovek ➔ lyudi)</div>
                    <div class="tr">= İnsan / İnsanlar</div>
                    <div class="details">Kökten değişen düzensiz çoğul[span_13](start_span)[span_13](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">друг ➔ друзья</div>
                    <div class="pron">(druk ➔ druz'ya)</div>
                    <div class="tr">= Arkadaş / Arkadaşlar</div>
                    <div class="details">-ЬЯ eki alan çoğul[span_14](start_span)[span_14](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">брат ➔ братья</div>
                    <div class="pron">(brat ➔ brat'ya)</div>
                    <div class="tr">= Erkek kardeş / Kardeşler</div>
                    <div class="details">-ЬЯ eki alan çoğul[span_15](start_span)[span_15](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">сын ➔ сыновья</div>
                    <div class="pron">(sın ➔ sınov'ya)</div>
                    <div class="tr">= Oğul / Oğullar</div>
                    <div class="details">-ЬЯ eki alan çoğul[span_16](start_span)[span_16](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">мать / дочь</div>
                    <div class="pron">(mat' / doç')</div>
                    <div class="tr">= Anne / Kız evlat</div>
                    <div class="details">Çoğul: матери / дочери[span_17](start_span)[span_17](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">крестьянин ➔ крестьяне</div>
                    <div class="pron">(krest'yanin ➔ krest'yane)</div>
                    <div class="tr">= Köylü / Köylüler</div>
                    <div class="details">-ин düşer, -АНЕ eklenir[span_18](start_span)[span_18](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">врач / учитель</div>
                    <div class="pron">(vraç / uçitel')</div>
                    <div class="tr">= Doktor / Öğretmen</div>
                    <div class="details">Meslek isimleri ve istisnalar[span_19](start_span)[span_19](end_span)</div>
                </div>
            </div>
        </section>

        <!-- 2. KISIM: MEKANLAR VE NESNELER -->
        <section class="category-section">
            <h2>2. Mekanlar, Eşyalar ve Nesneler</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">дом ➔ дома</div>
                    <div class="pron">(dom ➔ doma)</div>
                    <div class="tr">= Ev / Evler</div>
                    <div class="details">Eril, vurgu değişimi (-а)[span_20](start_span)[span_20](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">город ➔ города</div>
                    <div class="pron">(gorod ➔ goroda)</div>
                    <div class="tr">= Şehir / Şehirler</div>
                    <div class="details">Eril, vurgu değişimi (-а)[span_21](start_span)[span_21](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">окно ➔ окна</div>
                    <div class="pron">(akno ➔ okna)</div>
                    <div class="tr">= Pencere / Pencereler</div>
                    <div class="details">Nötr, -о ➔ -а kuralı[span_22](start_span)[span_22](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">море ➔ моря</div>
                    <div class="pron">(more ➔ morya)</div>
                    <div class="tr">= Deniz / Denizler</div>
                    <div class="details">Nötr, -е ➔ -я kuralı[span_23](start_span)[span_23](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">время ➔ времена</div>
                    <div class="pron">(vremya ➔ vremena)</div>
                    <div class="tr">= Zaman / Zamanlar</div>
                    <div class="details">-мя ile biten nötr istisna[span_24](start_span)[span_24](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">стул ➔ стулья</div>
                    <div class="pron">(stul ➔ stul'ya)</div>
                    <div class="tr">= Sandalye / Sandalyeler</div>
                    <div class="details">-ЬЯ eki alan özel çoğul[span_25](start_span)[span_25](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">дерево ➔ деревья</div>
                    <div class="pron">(derevo ➔ derev'ya)</div>
                    <div class="tr">= Ağaç / Ağaçlar</div>
                    <div class="details">-ЬЯ eki alan özel çoğul[span_26](start_span)[span_26](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">паспорт ➔ паспорта</div>
                    <div class="pron">(pasport ➔ pasporta)</div>
                    <div class="tr">= Pasaport / Pasaportlar</div>
                    <div class="details">Özel vurgulu çoğul (-а)[span_27](start_span)[span_27](end_span)</div>
                </div>
            </div>
        </section>

        <!-- 3. KISIM: SADECE TEKİL VE SADECE ÇOĞUL KELİMELER -->
        <section class="category-section">
            <h2>3. Sadece Tekil ve Sadece Çoğul Kullanılanlar</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">молоко / мясо / соль</div>
                    <div class="pron">(moloko / myaso / sol')</div>
                    <div class="tr">= Süt / Et / Tuz</div>
                    <div class="details">Daima tekil (Madde ve gıda ürünleri)[span_28](start_span)[span_28](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">мебель / одежда</div>
                    <div class="pron">(mebel' / odejda)</div>
                    <div class="tr">= Mobilya / Giysi</div>
                    <div class="details">Daima tekil (Topluluk isimleri)[span_29](start_span)[span_29](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">ножницы</div>
                    <div class="pron">(nojnıtsı)</div>
                    <div class="tr">= Makas</div>
                    <div class="details">Daima çoğul (Pluralia Tantum)[span_30](start_span)[span_30](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">очки / брюки / весы</div>
                    <div class="pron">(oçki / bryuki / vesı)</div>
                    <div class="tr">= Gözlük / Pantolon / Terazi</div>
                    <div class="details">Daima çoğul (Parçalı eşyalar)[span_31](start_span)[span_31](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">деньги / сутки / каникулы</div>
                    <div class="pron">(den'gi / sutki / kanikulı)</div>
                    <div class="tr">= Para / 24 Saat / Tatil</div>
                    <div class="details">Daima çoğul (Zaman ve soyut kavramlar)[span_32](start_span)[span_32](end_span)</div>
                </div>
            </div>
        </section>

        <!-- 4. KISIM: DEĞİŞMEYEN YABANCI KELİMELER -->
        <section class="category-section">
            <h2>4. Değişmeyen Yabancı Kelimeler (İndeklinabl)</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">пальто / кино / метро</div>
                    <div class="pron">(pal'to / kino / metro)</div>
                    <div class="tr">= Palto / Sinema / Metro</div>
                    <div class="details">Nötr, hiçbir ek almaz, değişmez[span_33](start_span)[span_33](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">кафе / такси / меню</div>
                    <div class="pron">(kafe / taksi / menyu)</div>
                    <div class="tr">= Kafe / Taksi / Menü</div>
                    <div class="details">Nötr, hiçbir ek almaz, değişmez[span_34](start_span)[span_34](end_span)</div>
                </div>
                <div class="word-card">
                    <div class="ru">жюри / интервью / пианино</div>
                    <div class="pron">(jyuri / interv'yu / pianino)</div>
                    <div class="tr">= Jüri / Röportaj / Piyano</div>
                    <div class="details">Nötr, hiçbir ek almaz, değişmez[span_35](start_span)[span_35](end_span)</div>
                </div>
            </div>
        </section>
    </main>

    <footer>
        <p>Rusça Eksiksiz Çalışma Defteri | GitHub İçin Hazırlandı 🖤🤍</p>
    </footer>

    <script>
        // Not kutusunu açıp kapatma fonksiyonu
        function toggleNotes() {
            const panel = document.getElementById('notesPanel');
            panel.classList.toggle('active');
        }

        // Anlık arama (Filtreleme) fonksiyonu
        function searchWords() {
            let input = document.getElementById('searchInput').value.toLowerCase();
            let cards = document.querySelectorAll('.word-card');

            cards.forEach(card => {
                let text = card.innerText.toLowerCase();
                if (text.includes(input)) {
                    card.style.display = "block";
                } else {
                    card.style.display = "none";
                }
            });
        }
    </script>
</body>
</html>

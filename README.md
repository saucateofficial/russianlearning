<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rusça Kelime ve Cümle Defterim</title>
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
            width: 350px;
            max-height: 450px;
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
            <h3>Önemli Kurallar & Notlar</h3>
            <ul>
                <li><strong>Nötr Ek Kuralı:</strong> <em>-o</em> ile bitenler çoğulda <em>-a</em> olur; <em>-e</em> ile bitenler çoğulda <em>-я</em> olur.[span_5](start_span)[span_5](end_span)</li>
                <li><strong>Vurgu Değişimi:</strong> Rusça kelimeler çoğul yapılırken vurgunun yeri (sesin yükseldiği hece) değişebilir (Örn: стол ➔ столы).[span_6](start_span)[span_6](end_span)</li>
                <li><strong>Tablo Doldurma Alıştırması (-и / -ы):</strong> -а / -я ile biten dişil kelimeler çoğul yapılırken -и ekini alır (auditoriya ➔ auditorii vb.).[span_7](start_span)[span_7](end_span)</li>
                <li><strong>İşaret Zamiri (Этo):</strong> Tekilde "Bu bir..." anlamı verirken, çoğul cümlelerde "Bunlar..." anlamına döner ve isimler de çoğul yapılır (Этo карандаш ➔ Это карандаши).[span_8](start_span)[span_8](end_span)[span_9](start_span)[span_9](end_span)</li>
            </ul>
        </div>
    </div>

    <header>
        <h1>Rusça Kelime ve Cümle Defterim</h1>
        <p class="subtitle">Yeni eklenen kurallar, çoklu gruplar ve tekil-çoğul cümle dönüşümleriyle güncellendi!</p>
    </header>

    <div class="search-box">
        <input type="text" id="searchInput" placeholder="Kelime veya cümle ara..." onkeyup="searchWords()">
    </div>

    <main id="contentArea">
        <!-- 1. KISIM: VURGU DEĞİŞİMLERİ VE ÇOĞULLAR -->
        <section class="category-section">
            <h2>Vurgu Değişimi Gösteren Kelimeler</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">дом ➔ дома</div>
                    <div class="pron">(dom ➔ doma)</div>
                    <div class="tr">= ev / evler</div>
                    <div class="details">Vurgu değişimi kuralı</div>
                </div>
                <div class="word-card">
                    <div class="ru">лес ➔ леса</div>
                    <div class="pron">(les ➔ lesa)</div>
                    <div class="tr">= orman / ormanlar</div>
                    <div class="details">Vurgu değişimi kuralı</div>
                </div>
                <div class="word-card">
                    <div class="ru">город ➔ города</div>
                    <div class="pron">(gorod ➔ goroda)</div>
                    <div class="tr">= şehir / şehirler</div>
                    <div class="details">Vurgu değişimi kuralı</div>
                </div>
                <div class="word-card">
                    <div class="ru">вечер ➔ вечера</div>
                    <div class="pron">(veçer ➔ veçera)</div>
                    <div class="tr">= akşam / akşamlar</div>
                    <div class="details">Vurgu değişimi kuralı</div>
                </div>
                <div class="word-card">
                    <div class="ru">поезд ➔ поезда</div>
                    <div class="pron">(poyezd ➔ poyezda)</div>
                    <div class="tr">= tren / trenler</div>
                    <div class="details">Vurgu değişimi kuralı</div>
                </div>
                <div class="word-card">
                    <div class="ru">язык ➔ языки</div>
                    <div class="pron">(yazık ➔ yaziki)</div>
                    <div class="tr">= dil, lisan</div>
                    <div class="details">Vurgu değişimi kuralı</div>
                </div>
            </div>
        </section>

        <!-- 2. KISIM: NÖTR KELİME ÇOĞULLARI -->
        <section class="category-section">
            <h2>Nötr İsimlerin Çoğul Halleri</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">письмо ➔ письма</div>
                    <div class="pron">(pismo ➔ pisma)</div>
                    <div class="tr">= mektup / mektuplar</div>
                    <div class="details">Nötr ek kuralı (-o ➔ -a)</div>
                </div>
                <div class="word-card">
                    <div class="ru">окно ➔ окна</div>
                    <div class="pron">(akno ➔ okna)</div>
                    <div class="tr">= pencere / pencereler</div>
                    <div class="details">Nötr ek kuralı (-o ➔ -a)</div>
                </div>
                <div class="word-card">
                    <div class="ru">место ➔ места</div>
                    <div class="pron">(mesto ➔ mesta)</div>
                    <div class="tr">= yer / mekan</div>
                    <div class="details">Nötr ek kuralı (-o ➔ -a)</div>
                </div>
                <div class="word-card">
                    <div class="ru">поле ➔ поля</div>
                    <div class="pron">(pole ➔ polya)</div>
                    <div class="tr">= tarla / saha</div>
                    <div class="details">Nötr ek kuralı (-e ➔ -я)</div>
                </div>
                <div class="word-card">
                    <div class="ru">море ➔ моря</div>
                    <div class="pron">(more ➔ morya)</div>
                    <div class="tr">= deniz / denizler</div>
                    <div class="details">Nötr ek kuralı (-e ➔ -я)</div>
                </div>
                <div class="word-card">
                    <div class="ru">здание ➔ здания</div>
                    <div class="pron">(zdaniye ➔ zdaniya)</div>
                    <div class="tr">= bina / binalar</div>
                    <div class="details">Nötr ek kuralı (-e ➔ -я)</div>
                </div>
            </div>
        </section>

        <!-- 3. KISIM: ÇOKLU İSİM GRUPLARI -->
        <section class="category-section">
            <h2>Çoklu İsim Grupları ve Çoğullaştırma</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">шкаф, стол и стул</div>
                    <div class="pron">(şkaf, stol i stul)</div>
                    <div class="tr">➔ шкафы, столы и стулья<br>= dolap, masa ve sandalye</div>
                    <div class="details">Çoklu grup örneği</div>
                </div>
                <div class="word-card">
                    <div class="ru">товарищ и друг</div>
                    <div class="pron">(tavariç i druk)</div>
                    <div class="tr">➔ товарищи и друзья<br>= yoldaş ve arkadaş</div>
                    <div class="details">Çoklu grup örneği</div>
                </div>
                <div class="word-card">
                    <div class="ru">сестра, брат и сын</div>
                    <div class="pron">(sistra, brat i sın)</div>
                    <div class="tr">➔ сёстры, братья и сыновья<br>= kız kardeş, erkek kardeş ve oğul</div>
                    <div class="details">Çoklu grup örneği</div>
                </div>
                <div class="word-card">
                    <div class="ru">книга, тетрадь и словарь</div>
                    <div class="pron">(kniga, tetrat i slovar)</div>
                    <div class="tr">➔ книги, тетради и словари<br>= kitap, defter ve sözlük</div>
                    <div class="details">Çoklu grup örneği</div>
                </div>
            </div>
        </section>

        <!-- 4. KISIM: CÜMLELERİ TEKİLDEN ÇOĞULA ÇEVİRME -->
        <section class="category-section">
            <h2>Cümleleri Tekilden Çoğula Çevirme Pratikleri</h2>
            <div class="word-grid">
                <div class="word-card">
                    <div class="ru">Это карандаш</div>
                    <div class="pron">(Eta karandaş)</div>
                    <div class="tr">➔ Это карандаши<br>= Bu bir kurşun kalem ➔ Bunlar kurşun kalemdir</div>
                    <div class="details">Tekil / Çoğul Cümle Dönüşümü</div>
                </div>
                <div class="word-card">
                    <div class="ru">Это аудитория</div>
                    <div class="pron">(Eta auditoriya)</div>
                    <div class="tr">➔ Это аудитории<br>= Bu bir dersliktir ➔ Bunlar dersliktir</div>
                    <div class="details">Tekil / Çoğul Cümle Dönüşümü</div>
                </div>
                <div class="word-card">
                    <div class="ru">Это лампа</div>
                    <div class="pron">(Eta lampa)</div>
                    <div class="tr">➔ Это лампы<br>= Bu bir lambadır ➔ Bunlar lambadır</div>
                    <div class="details">Tekil / Çoğul Cümle Dönüşümü</div>
                </div>
                <div class="word-card">
                    <div class="ru">Это костюм</div>
                    <div class="pron">(Eta kostyum)</div>
                    <div class="tr">➔ Это костюмы<br>= Bu takım elbise ➔ Bunlar takım elbise</div>
                    <div class="details">Tekil / Çoğul Cümle Dönüşümü</div>
                </div>
                <div class="word-card">
                    <div class="ru">Это ребёнок</div>
                    <div class="pron">(Eta rebyonok)</div>
                    <div class="tr">➔ Это дети<br>= Bu bir çocuk ➔ Bunlar çocuklar</div>
                    <div class="details">Düzensiz çoğul cümle dönüşümü</div>
                </div>
                <div class="word-card">
                    <div class="ru">Это человек</div>
                    <div class="pron">(Eta çelovek)</div>
                    <div class="tr">➔ Это люди<br>= Bu bir insan ➔ Bunlar insanlar</div>
                    <div class="details">Düzensiz çoğul cümle dönüşümü</div>
                </div>
            </div>
        </section>
    </main>

    <footer>
        <p>Rusça Kapsamlı Çalışma Notları | GitHub için Hazırlandı 🖤🤍</p>
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

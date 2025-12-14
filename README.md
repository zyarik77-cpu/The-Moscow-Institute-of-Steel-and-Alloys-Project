
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Орки Warhammer 40,000: Экосистема и Иерархия</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Russo+One&family=Roboto+Condensed:wght@400;700&display=swap');

        body {
            font-family: 'Roboto Condensed', sans-serif;
            background-color: #f5f5f0;
            color: #1a202c;
        }

        h1, h2, h3, .ork-font {
            font-family: 'Russo One', sans-serif;
            text-transform: uppercase;
        }

        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }

        .active-tab {
            background-color: #4a7c59;
            color: white;
            border-bottom: 4px solid #2f5238;
        }

        .inactive-tab {
            background-color: #e2e8f0;
            color: #4a5568;
            border-bottom: 4px solid #cbd5e0;
        }
        
        .inactive-tab:hover {
            background-color: #cbd5e0;
        }

        .card-shadow {
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        .unit-button {
            width: 100%;
            text-align: left;
            padding: 0.75rem;
            border-radius: 0.25rem;
            transition: all 0.2s;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border: 1px solid #e2e8f0;
            background-color: white;
            cursor: pointer;
        }

        .unit-button:hover {
            background-color: #f7fafc;
        }

        .unit-button.active {
            background-color: #f0fff4;
            font-weight: bold;
            border-left: 4px solid #16a34a;
            box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1);
        }

        .unit-button .unit-role {
            font-size: 0.75rem;
            color: #94a3b8;
            background-color: #f1f5f9;
            padding: 0.25rem 0.5rem;
            border-radius: 0.25rem;
        }

        .detail-tag {
            padding: 0.25rem 0.5rem;
            background-color: #e2e8f0;
            color: #334155;
            font-size: 0.75rem;
            font-weight: bold;
            text-transform: uppercase;
            border-radius: 0.25rem;
        }

        .container-main {
            max-width: 1280px;
            margin-left: auto;
            margin-right: auto;
            padding-left: 2rem;
            padding-right: 2rem;
        }

        .header-container {
            max-width: 1280px;
            margin-left: auto;
            margin-right: auto;
            padding-left: 2rem;
            padding-right: 2rem;
            height: 4rem;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .header-nav {
            display: flex;
            align-items: center;
            gap: 0.75rem;
        }

        .header {
            background-color: #1e293b;
            color: white;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            position: sticky;
            top: 0;
            z-index: 50;
        }

        .nav-links {
            display: flex;
            gap: 1rem;
            font-size: 0.875rem;
            font-weight: bold;
        }

        .nav-link {
            transition: color 0.2s;
        }

        .nav-link:hover {
            color: #4ade80;
        }

        .header-logo {
            font-size: 1.875rem;
            letter-spacing: 0.05em;
            color: #22c55e;
        }

        .header-subtitle {
            font-size: 0.875rem;
            color: #94a3b8;
            display: block;
        }

        .hero-title {
            font-size: 3.75rem;
            text-align: center;
            letter-spacing: 0.1em;
        }

        .hero-title-ork {
            color: #22c55e;
        }

        .section-title {
            font-size: 1.875rem;
            color: #1e293b;
            margin-bottom: 1rem;
        }

        .section-title-large {
            font-size: 1.875rem;
            color: #1e293b;
            margin-bottom: 0.5rem;
        }

        .section-title-border {
            border-bottom: 1px solid #e2e8f0;
            padding-bottom: 0.5rem;
        }

        .card-title {
            font-size: 1.25rem;
            color: #15803d;
            margin-bottom: 0.5rem;
        }

        .card-title-small {
            font-size: 0.875rem;
            font-weight: bold;
            color: #64748b;
            text-transform: uppercase;
            margin-bottom: 0.75rem;
        }

        .hero-section {
            background-color: #0f172a;
            color: white;
            padding-top: 4rem;
            padding-bottom: 4rem;
            margin-bottom: 2rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }

        .section-card {
            background-color: white;
            border-radius: 0.5rem;
            padding: 2rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            border-left: 8px solid #16a34a;
        }

        .section-card-simple {
            background-color: white;
            border-radius: 0.5rem;
            padding: 1.5rem;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        .section-card-centered {
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .chart-title {
            font-size: 1.25rem;
            text-align: center;
            font-weight: bold;
            margin-bottom: 0.5rem;
        }

        .chart-subtitle {
            text-align: center;
            font-size: 0.75rem;
            color: #64748b;
            margin-bottom: 1rem;
        }

        .chart-footer {
            margin-top: 1rem;
            font-size: 0.75rem;
            text-align: center;
            color: #94a3b8;
            font-style: italic;
        }

        .info-card {
            background-color: #f8fafc;
            padding: 1.5rem;
            border-radius: 0.25rem;
            border: 1px solid #e2e8f0;
        }

        .info-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1.5rem;
        }

        .biology-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 2rem;
        }

        .hierarchy-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 2rem;
        }

        .text-hero {
            text-align: center;
            font-size: 1.25rem;
            color: #94a3b8;
            margin-top: 1rem;
            font-weight: bold;
        }

        .text-section {
            font-size: 1.125rem;
            color: #475569;
            margin-bottom: 1.5rem;
            line-height: 1.75;
        }

        .text-card {
            font-size: 0.875rem;
            color: #475569;
        }

        .text-description {
            color: #1e293b;
            line-height: 1.75;
        }

        .text-intro {
            color: #475569;
            margin-bottom: 1rem;
        }

        .tab-button {
            padding: 0.75rem 1.5rem;
            font-weight: bold;
            font-size: 0.875rem;
            border-radius: 0.5rem 0.5rem 0 0;
            transition: all 0.2s;
        }

        .unit-detail-card {
            background-color: #f0fdf4;
            padding: 1.5rem;
            border-radius: 0.25rem;
            border-left: 4px solid #16a34a;
            display: flex;
            flex-direction: row;
            align-items: flex-start;
            gap: 1.5rem;
        }

        .unit-image-wrapper {
            flex-shrink: 0;
        }

        .unit-image {
            width: 8rem;
            height: 8rem;
            border-radius: 9999px;
            object-fit: cover;
            border: 4px solid #15803d;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }

        .unit-detail-title {
            font-size: 1.5rem;
            color: #166534;
            margin-bottom: 0.5rem;
            margin-top: 0;
        }

        .tags-container {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            margin-bottom: 0.75rem;
        }

        .stats-card {
            background-color: white;
            border: 1px solid #f1f5f9;
            border-radius: 0.25rem;
            padding: 1rem;
            box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
        }

        .stats-title {
            font-size: 0.875rem;
            font-weight: bold;
            color: #64748b;
            text-transform: uppercase;
            margin-bottom: 0.5rem;
            text-align: center;
        }

        .unit-list-container {
            background-color: #f8fafc;
            border-radius: 0.25rem;
            border: 1px solid #e2e8f0;
            padding: 1rem;
            height: 100%;
        }

        .unit-list {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }

        .religion-section {
            background-color: #1e293b;
            color: white;
            border-radius: 0.5rem;
            padding: 2rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }

        .religion-section-title {
            font-size: 1.875rem;
            text-align: center;
            margin-bottom: 2rem;
        }

        .vs-container {
            display: flex;
            position: absolute;
            inset: 0;
            align-items: center;
            justify-content: center;
            pointer-events: none;
        }

        .religion-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 2rem;
            position: relative;
        }

        .religion-card {
            background-color: #334155;
            padding: 1.5rem;
            border-radius: 0.5rem;
            text-align: center;
            transition: background-color 0.3s;
            border-bottom: 4px solid #ef4444;
        }

        .religion-card:hover {
            background-color: #475569;
        }

        .religion-card-blue {
            border-bottom-color: #3b82f6;
            margin-top: 0;
        }

        .religion-title {
            font-size: 2.25rem;
            margin-bottom: 0.5rem;
        }

        .religion-subtitle {
            color: #f87171;
            font-weight: bold;
            margin-bottom: 1rem;
            text-transform: uppercase;
            font-size: 0.875rem;
        }

        .religion-subtitle-blue {
            color: #60a5fa;
        }

        .religion-quote {
            color: #cbd5e1;
            font-style: italic;
            margin-bottom: 1rem;
        }

        .religion-desc {
            font-size: 0.875rem;
            color: #94a3b8;
        }

        .vs-badge {
            background-color: #dc2626;
            color: white;
            font-weight: 900;
            border-radius: 9999px;
            width: 3rem;
            height: 3rem;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 4px solid #1e293b;
            z-index: 10;
            font-size: 1.25rem;
            position: absolute;
            inset: 0;
            margin: auto;
            pointer-events: none;
        }

        .footer {
            text-align: center;
            color: #94a3b8;
            font-size: 0.875rem;
            padding-top: 2rem;
            padding-bottom: 2rem;
            border-top: 1px solid #cbd5e0;
        }

        .footer-text {
            margin-top: 0.5rem;
        }

        .life-cycle-item {
            display: flex;
            align-items: flex-start;
            cursor: default;
        }

        .life-cycle-number {
            background-color: #dcfce7;
            padding: 0.75rem;
            border-radius: 9999px;
            margin-right: 1rem;
            transition: background-color 0.2s;
        }

        .life-cycle-item:hover .life-cycle-number {
            background-color: #bbf7d0;
        }

        .life-cycle-number-active {
            background-color: #16a34a;
            color: white;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }

        .life-cycle-title {
            font-weight: bold;
            color: #1e293b;
        }

        .life-cycle-text {
            font-size: 0.875rem;
            color: #64748b;
        }

        .life-cycle-text-green {
            color: #15803d;
        }

        .section-divider {
            display: flex;
            flex-wrap: wrap;
            border-bottom: 1px solid #e2e8f0;
            margin-bottom: 1.5rem;
            gap: 0.5rem;
        }

        .main-content {
            padding-top: 2rem;
            padding-bottom: 2rem;
            display: flex;
            flex-direction: column;
            gap: 3rem;
        }

        .section-spacing {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }

        .detail-section {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            grid-column: span 2;
        }

        .list-section {
            grid-column: span 1;
        }
    </style>

</head>
<body class="antialiased">

    <header class="header">
        <div class="header-container">
            <div class="header-nav">
                <span class="header-logo ork-font">WAAAGH!</span>
                <span class="header-subtitle">Архив Империума: Ксенос Оркоиды</span>
            </div>
            <nav class="nav-links">
                <button onclick="scrollToSection('origin')" class="nav-link">Происхождение</button>
                <button onclick="scrollToSection('biology')" class="nav-link">Биология</button>
                <button onclick="scrollToSection('hierarchy')" class="nav-link">Иерархия</button>
            </nav>
        </div>
    </header>

    <div class="hero-section">
        <div class="container-main">
            <h1 class="hero-title ork-font hero-title-ork">
                ОРКИ В WARHAMMER 40 000
            </h1>
            <p class="text-hero">WAAAGH! Прибыл.</p>
        </div>
    </div>
    <main class="container-main main-content">

        <section id="origin" class="section-card">
            <h2 class="section-title">Происхождение и Природа</h2>
            <p class="text-section">
                Орки — это не результат эволюции, а совершенное биологическое оружие. Этот раздел раскрывает их древнюю историю, связь с исчезнувшими Древними и уникальную природу, сочетающую черты животных и грибов.
            </p>
            
            <div class="info-grid">
                <div class="info-card">
                    <h3 class="card-title">Создание</h3>
                    <p class="text-card">60 миллионов лет назад Древние ("Мозгобойзы") создали Крорков для войны с Некронами в ходе "Войны в Небесах".</p>
                </div>
                <div class="info-card">
                    <h3 class="card-title">Деградация</h3>
                    <p class="text-card">Могучие Крорки деградировали до нынешних Орков, сохранив лишь инстинкты войны («Waaagh!») и генетическое знание технологий.</p>
                </div>
                <div class="info-card">
                    <h3 class="card-title">Симбиоз</h3>
                    <p class="text-card">Орки — это симбиоз животного и гриба (Algae). Размножаются спорами, создавая автономную экосистему на любой планете.</p>
                </div>
            </div>
        </section>

        <section id="biology" class="biology-grid">
            <div class="section-card-simple">
                <h2 class="section-title-large section-title-border">Споровый Цикл Жизни</h2>
                <p class="text-intro">
                    Визуализация этапов развития орочьей экосистемы. От микроскопической споры до полноценной армии.
                </p>
                <div class="space-y-4">
                    <div class="life-cycle-item">
                        <div class="life-cycle-number">1</div>
                        <div>
                            <h4 class="life-cycle-title">Выброс Спор</h4>
                            <p class="life-cycle-text">Постоянно в течение жизни, массово — при смерти. "Вечная перхоть" войны.</p>
                        </div>
                    </div>
                    <div class="life-cycle-item">
                        <div class="life-cycle-number">2</div>
                        <div>
                            <h4 class="life-cycle-title">Мицелий</h4>
                            <p class="life-cycle-text">Подземная грибница, подготавливающая биосферу.</p>
                        </div>
                    </div>
                    <div class="life-cycle-item">
                        <div class="life-cycle-number">3</div>
                        <div>
                            <h4 class="life-cycle-title">Сквиги и Грибы</h4>
                            <p class="life-cycle-text">Первые всходы: еда (грибы) и фауна (сквиги).</p>
                        </div>
                    </div>
                    <div class="life-cycle-item">
                        <div class="life-cycle-number">4</div>
                        <div>
                            <h4 class="life-cycle-title">Снотлинги и Гретчины</h4>
                            <p class="life-cycle-text">Рабочая сила для создания инфраструктуры поселения.</p>
                        </div>
                    </div>
                    <div class="life-cycle-item">
                        <div class="life-cycle-number life-cycle-number-active">5</div>
                        <div>
                            <h4 class="life-cycle-title life-cycle-text-green">Появление Орков</h4>
                            <p class="life-cycle-text">Воины выходят на поверхность, когда всё готово для войны.</p>
                        </div>
                    </div>
                </div>
            </div>

            <div class="section-card-simple section-card-centered">
                <h3 class="chart-title">Состав Оркоидной Популяции (Процентное Распределение)</h3>
                <p class="chart-subtitle">Относительное количество особей в типичном Waaagh! (включая фауну)</p>
                <div class="chart-container">
                    <canvas id="ecosystemChart"></canvas>
                </div>
                <p class="chart-footer">Сдвиг в сторону "Парней" означает созревание Waaagh!.</p>
            </div>
        </section>
        <section id="hierarchy" class="section-spacing">
            <div class="section-card">
                <div class="mb-8">
                    <h2 class="section-title">Иерархия Зеленокожих</h2>
                    <p class="text-slate-600">
                        Исследуйте различные касты орков. Выберите категорию ниже, чтобы увидеть характеристики, роли и сравнение боевой мощи.
                    </p>
                </div>

                <div class="section-divider">
                    <button class="tab-button active-tab" id="tab-low" onclick="switchTab('low')">Низшие Формы</button>
                    <button class="tab-button inactive-tab" id="tab-main" onclick="switchTab('main')">Армия (Парни)</button>
                    <button class="tab-button inactive-tab" id="tab-odd" onclick="switchTab('odd')">Чудаки (Спецы)</button>
                    <button class="tab-button inactive-tab" id="tab-elite" onclick="switchTab('elite')">Элита и Лидеры</button>
                </div>

                <div class="hierarchy-grid">
                    <div class="list-section unit-list-container">
                        <h4 class="card-title-small">Список Видов</h4>
                        <div id="unit-list" class="unit-list">
                        </div>
                    </div>

                    <div class="detail-section">
                        <div class="unit-detail-card">
                            <div class="unit-image-wrapper">
                                <img id="detail-image" src="" alt="Изображение юнита" class="unit-image">
                            </div>
                            <div>
                                <h3 id="detail-title" class="unit-detail-title ork-font">Выберите вид</h3>
                                <div class="tags-container" id="detail-tags">
                                </div>
                                <p id="detail-desc" class="text-description">
                                    Нажмите на элемент слева, чтобы узнать подробности.
                                </p>
                            </div>
                        </div>

                        <div class="stats-card">
                            <h4 class="stats-title">Анализ Боевой Эффективности</h4>
                            <div class="chart-container" style="height: 250px;">
                                <canvas id="statsChart"></canvas>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="religion-section">
            <h2 class="religion-section-title">Религия: Битва Богов</h2>
            <div class="religion-grid">
                <div class="vs-container">
                    <div class="vs-badge">VS</div>
                </div>

                <div class="religion-card">
                    <h3 class="religion-title ork-font">ГОРК</h3>
                    <p class="religion-subtitle">Жестокий, но хитрый</p>
                    <p class="religion-quote">"Я тебя вижу, я иду к тебе, я тебя стукаю."</p>
                    <p class="religion-desc">Бог грубой силы. Покровитель Воинов и Варбоссов, предпочитающих лобовую атаку.</p>
                </div>
                <div class="religion-card religion-card-blue">
                    <h3 class="religion-title ork-font">МОРК</h3>
                    <p class="religion-subtitle religion-subtitle-blue">Хитрый, но жестокий</p>
                    <p class="religion-quote">"Я жду, пока ты отвлечешься, а потом стукаю тебя."</p>
                    <p class="religion-desc">Бог коварства. Покровитель Меков и Коммандос, ценящих тактику и технологии.</p>
                </div>
            </div>
        </section>

        <footer class="footer">
            <p>"Зеленый — значит лучший!" — Орочья мудрость.</p>
            <p class="footer-text">Генерация данных на основе отчета Магос Биологис.</p>
        </footer>

    </main>

    <script>
        const orkData = {
            low: [
                {
                    id: 'squig',
                    name: 'Сквиги',
                    role: 'Фауна / Еда / Оружие',
                    desc: 'Простейшая форма жизни. Состоят из пасти и ног. Виды: Съедобные (еда), Парики (волосы), Взрывные (мины), Сквигготы (гигантские танки), Лицееды (спорт).',
                    stats: { str: 2, int: 1, aggro: 7 },
                    tags: ['Еда', 'Зверь'],
                    imageUrl: 'https://avatars.mds.yandex.net/get-mpic/4343038/img_id8714809864024839628.jpeg/orig'
                },
                {
                    id: 'snotling',
                    name: 'Снотлинги',
                    role: 'Агрокультура / Боеприпасы',
                    desc: 'Самые мелкие и глупые. Выращивают грибы. Используются как живые снаряды для Шоковой Атакующей Пушки (Shokk Attack Gun), телепортируясь внутрь врага.',
                    stats: { str: 1, int: 2, aggro: 3 },
                    tags: ['Раб', 'Еда', 'Патроны'],
                    imageUrl: 'https://www.warhammer.com/app/resources/catalog/product/threeSixty/99120909004_BBCrudCreekNosepickersTeamSpin5360/01.jpg?fm=webp&w=670'
                },
                {
                    id: 'gretchin',
                    name: 'Гретчины ',
                    role: 'Слуги / Артиллерия',
                    desc: 'Хитрые, но слабые. Слуги, повара, помощники Меков. Благодаря мелким пальцам отлично управляют артиллерией. Часто служат живым щитом.',
                    stats: { str: 2, int: 5, aggro: 2 },
                    tags: ['Слуга', 'Стрелок'],
                    imageUrl: 'https://www.warhammer.com/app/resources/catalog/product/threeSixty/99120103053_OrkGretchin3360/01.jpg?fm=webp&w=670'
                }
            ],
            main: [
                {
                    id: 'slugga',
                    name: 'Слагга-бойз',
                    role: 'Ближний бой',
                    desc: 'Основная пехота. Вооружены пистолетом (слаггой) и грубым рубилом (чоппой). Любят наваливаться толпой.',
                    stats: { str: 6, int: 3, aggro: 9 },
                    tags: ['Пехота', 'Ближний бой'],
                    imageUrl: 'https://i.pinimg.com/originals/f0/c3/85/f0c38552e7cea46399088ceb27268c66.png'
                },
                {
                    id: 'shoota',
                    name: 'Шута-бойз',
                    role: 'Огневая поддержка',
                    desc: 'Любят громкие звуки. Вооружены тяжелыми пулеметами (шуты). Точность низкая, но плотность огня ("стенка свинца") колоссальная.',
                    stats: { str: 6, int: 3, aggro: 7 },
                    tags: ['Пехота', 'Стрельба'],
                    imageUrl: 'https://i.pinimg.com/originals/c5/f3/81/c5f381fa6523134b309b925db337c62a.jpg'
                }
            ],
            odd: [
                {
                    id: 'mek',
                    name: 'Мекбойзы',
                    role: 'Инженеры',
                    desc: 'Генетическое знание техники. Собирают танки из мусора. Не знают физику, но знают "шоб стреляло".',
                    stats: { str: 6, int: 8, aggro: 5 },
                    tags: ['Техника', 'Крафт'],
                    imageUrl: 'https://avatars.mds.yandex.net/i?id=2340fbffee88076ccab4f058aaf6c629_l-5219731-images-thumbs&n=13'
                },
                {
                    id: 'doc',
                    name: 'Пейнбойзы',
                    role: 'Медицина',
                    desc: 'Орочьи хирурги. Лечение включает удары молотком (анестезия) и пришивание бионических конечностей.',
                    stats: { str: 7, int: 6, aggro: 6 },
                    tags: ['Лечение', 'Бионика'],
                    imageUrl: 'https://main-cdn.sbermegamarket.ru/big1/hlr-system/-30/122/107/511/231/823/100042485531b0.jpg'
                },
                {
                    id: 'weird',
                    name: 'Вейрдбойзы',
                    role: 'Псайкеры',
                    desc: 'Живые проводники энергии Waaagh!. Могут взорвать врага молнией или случайно взорвать свою голову, если рядом слишком много орущих орков.',
                    stats: { str: 5, int: 9, aggro: 8 },
                    tags: ['Магия', 'Варп'],
                    imageUrl: 'https://i.pinimg.com/474x/1b/57/7c/1b577c934080b25b2610562073edf611.jpg'
                }
            ],
            elite: [
                {
                    id: 'nob',
                    name: 'Нобы',
                    role: 'Командиры отрядов',
                    desc: 'Больше и сильнее обычных парней. Поддерживают дисциплину ударами кулаков. Имеют лучшее снаряжение.',
                    stats: { str: 8, int: 5, aggro: 9 },
                    tags: ['Элита', 'Командир'],
                    imageUrl: 'https://main-cdn.sbermegamarket.ru/big2/hlr-system/645/006/228/107/164/0/100071142812b3.jpg'
                },
                {
                    id: 'meganob',
                    name: 'Меганобы',
                    role: 'Тяжелая Элита',
                    desc: 'Нобы в сверхтяжелой Мега-броне. Медленные, но превращаются в ходячие танки.',
                    stats: { str: 9, int: 5, aggro: 8 },
                    tags: ['Танк', 'Броня'],
                    imageUrl: 'https://avatars.mds.yandex.net/i?id=0092d8013bbd90986b52d1457d029d65_l-3613310-images-thumbs&n=13'
                },
                {
                    id: 'warboss',
                    name: 'ВАРБОСС',
                    role: 'Лидер WAAAGH!',
                    desc: 'Вершина пищевой цепи. Огромный (3-4 метра), невероятно сильный. Единоличный правитель, способный разорвать танк руками.',
                    stats: { str: 10, int: 9, aggro: 10 },
                    tags: ['Лидер', 'Монстр'],
                    imageUrl: 'https://avatars.mds.yandex.net/get-mpic/13480750/2a00000193bcfe76d4f344ed0e6ed9877796/orig'
                }
            ]
        };

        const populationData = {
            labels: ['Сквиги (Фауна/Еда)', 'Гретчины/Сноты (Слуги)', 'Парни (Бойзы)', 'Нобы/Спецы', 'Варбоссы '],
            data: [50, 35, 12, 2.5, 0.5],
            colors: ['#e53e3e', '#d69e2e', '#38a169', '#2f855a', '#1a202c']
        };

        let currentTab = 'low';
        let currentUnitIndex = 0;
        let ecosystemChartInstance = null;
        let statsChartInstance = null;

        document.addEventListener('DOMContentLoaded', () => {
            initEcosystemChart();
            initStatsChart();
            switchTab('low');
        });

        function scrollToSection(id) {
            document.getElementById(id).scrollIntoView({ behavior: 'smooth' });
        }

        function switchTab(category) {
            currentTab = category;

            const tabs = ['low', 'main', 'odd', 'elite'];
            tabs.forEach(t => {
                const btn = document.getElementById(`tab-${t}`);
                if (t === category) {
                    btn.classList.remove('inactive-tab');
                    btn.classList.add('active-tab');
                } else {
                    btn.classList.remove('active-tab');
                    btn.classList.add('inactive-tab');
                }
            });

            renderUnitList(category);
            
            selectUnit(0);
        }

        function renderUnitList(category) {
            const listContainer = document.getElementById('unit-list');
            listContainer.innerHTML = '';
            
            orkData[category].forEach((unit, index) => {
                const btn = document.createElement('button');
                btn.className = `unit-button ${index === 0 ? 'active' : ''}`;
                btn.onclick = () => selectUnit(index);
                btn.innerHTML = `
                    <span>${unit.name}</span>
                    <span class="unit-role">${unit.role}</span>
                `;
                btn.id = `unit-btn-${index}`;
                listContainer.appendChild(btn);
            });
        }

        function selectUnit(index) {
            currentUnitIndex = index;
            const unit = orkData[currentTab][index];

            const allBtns = document.getElementById('unit-list').children;
            Array.from(allBtns).forEach((btn, i) => {
                if (i === index) {
                    btn.className = 'unit-button active';
                } else {
                    btn.className = 'unit-button';
                }
            });

            document.getElementById('detail-title').innerText = unit.name;
            document.getElementById('detail-desc').innerText = unit.desc;
            document.getElementById('detail-image').src = unit.imageUrl;
            document.getElementById('detail-image').alt = `Изображение ${unit.name}`;
            
            const tagContainer = document.getElementById('detail-tags');
            tagContainer.innerHTML = '';
            unit.tags.forEach(tag => {
                const span = document.createElement('span');
                span.className = 'detail-tag';
                span.innerText = tag;
                tagContainer.appendChild(span);
            });

            updateStatsChart(unit);
        }

        function initEcosystemChart() {
            const ctx = document.getElementById('ecosystemChart').getContext('2d');
            ecosystemChartInstance = new Chart(ctx, {
                type: 'pie', 
                data: {
                    labels: populationData.labels,
                    datasets: [{
                        data: populationData.data,
                        backgroundColor: populationData.colors,
                        borderWidth: 0
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'right',
                            labels: {
                                font: { size: 10 },
                                boxWidth: 12
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    let label = context.label || '';
                                    if (label) {
                                        label += ': ';
                                    }
                                    if (context.parsed !== null) {
                                        label += context.parsed.toFixed(1) + '%';
                                    }
                                    return label;
                                }
                            }
                        }
                    }
                }
            });
        }

        function initStatsChart() {
            const ctx = document.getElementById('statsChart').getContext('2d');
            statsChartInstance = new Chart(ctx, {
                type: 'bar',
                data: {
                    labels: ['Сила (Power)', 'Интеллект/Хитрость', 'Агрессия'],
                    datasets: [{
                        label: 'Характеристики (макс. 10)',
                        data: [0, 0, 0],
                        backgroundColor: ['#c05621', '#2b6cb0', '#e53e3e']
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    indexAxis: 'y',
                    scales: {
                        x: {
                            beginAtZero: true,
                            max: 10,
                            grid: { display: false }
                        },
                        y: {
                            grid: { display: false }
                        }
                    },
                    plugins: {
                        legend: { display: false }
                    }
                }
            });
        }

        function updateStatsChart(unit) {
            if (!statsChartInstance) return;
            
            statsChartInstance.data.datasets[0].data = [unit.stats.str, unit.stats.int, unit.stats.aggro];
            statsChartInstance.update();
        }

    </script>
</body>
</html>
</html>

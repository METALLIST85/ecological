<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Сохранение экологии</title>

<!-- Leaflet карта -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<style>
    :root{
        --bg: linear-gradient(to bottom, #e8f5e9, #ffffff);
        --text: #1b1b1b;
        --card: white;
        --accent: #2e7d32;
        --nav: #1b5e20;
        --header1: #2e7d32;
        --header2: #66bb6a;
    }

    body.dark{
        --bg: linear-gradient(to bottom, #0d1b12, #111);
        --text: #eaeaea;
        --card: #1e1e1e;
        --accent: #81c784;
        --nav: #0b2e14;
        --header1: #1b5e20;
        --header2: #2e7d32;
    }

    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background: var(--bg);
        color: var(--text);
        transition: 0.4s ease;
    }

    header {
        background: linear-gradient(135deg, var(--header1), var(--header2));
        color: white;
        padding: 40px 20px;
        text-align: center;
        position: relative;
    }

    header h1 {
        margin: 0;
        font-size: 36px;
    }

    .toggle {
        position: absolute;
        top: 20px;
        right: 20px;
        background: white;
        border: none;
        padding: 10px 15px;
        border-radius: 8px;
        cursor: pointer;
        font-weight: bold;
    }

    body.dark .toggle{
        background: #333;
        color: white;
    }

    nav {
        display: flex;
        justify-content: center;
        background: var(--nav);
        padding: 10px;
    }

    nav a {
        color: white;
        margin: 0 15px;
        text-decoration: none;
        font-weight: bold;
    }

    section {
        padding: 40px 20px;
        max-width: 1000px;
        margin: auto;
    }

    .card {
        background: var(--card);
        padding: 20px;
        margin: 15px 0;
        border-radius: 12px;
        box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        opacity: 0;
        transform: translateY(30px);
        transition: all 0.8s ease;
    }

    .card.show {
        opacity: 1;
        transform: translateY(0);
    }

    #map {
        height: 500px;
        border-radius: 12px;
        margin-top: 15px;
    }

    footer {
        text-align: center;
        padding: 20px;
        background: var(--nav);
        color: white;
        margin-top: 40px;
    }

    h2 {
        color: var(--accent);
    }
</style>
</head>

<body>

<header>
    <button class="toggle" onclick="toggleTheme()">🌙 Тема</button>
    <h1>Сохранение экологии</h1>
    <p>Наш вклад в чистое и безопасное будущее планеты</p>
</header>

<nav>
    <a href="#eco">Что такое экология</a>
    <a href="#problems">Проблемы</a>
    <a href="#tasks">Задачи</a>
    <a href="#mapSection">Карта проблем</a>
</nav>

<section id="eco">
    <div class="card">
        <h2>Что такое экология?</h2>
        <p>
            Экология — это наука, которая изучает взаимоотношения живых организмов между собой и с окружающей средой.
            Она помогает понять, как деятельность человека влияет на природу и как сохранить природные ресурсы для будущих поколений.
        </p>
    </div>
</section>

<section id="problems">
    <div class="card">
        <h2>Основные экологические проблемы</h2>
        <ul>
            <li>Загрязнение воздуха и воды</li>
            <li>Вырубка лесов</li>
            <li>Накопление пластиковых отходов</li>
            <li>Глобальное потепление</li>
            <li>Исчезновение видов животных и растений</li>
        </ul>
    </div>
</section>

<section id="tasks">
    <div class="card">
        <h2>Основные задачи по сохранению экологии</h2>
        <ul>
            <li>Сокращение использования пластика</li>
            <li>Переработка и сортировка отходов</li>
            <li>Сохранение лесов и озеленение территорий</li>
            <li>Использование экологически чистого транспорта</li>
            <li>Экономия воды и электроэнергии</li>
            <li>Повышение экологической грамотности населения</li>
        </ul>
    </div>
</section>

<section id="mapSection">
    <div class="card">
        <h2>Интерактивная карта экологических проблем</h2>
        <p>Ключевые экологические зоны планеты</p>
        <div id="map"></div>
    </div>
</section>

<footer>
    <p>© 2026 Экологический сайт. Береги природу!</p>
</footer>

<script>
const cards = document.querySelectorAll('.card');

const observer = new IntersectionObserver(entries => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('show');
        }
    });
}, { threshold: 0.2 });

cards.forEach(card => observer.observe(card));

function toggleTheme(){
    document.body.classList.toggle('dark');
}

// Карта
var map = L.map('map').setView([20, 0], 2);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap'
}).addTo(map);

const zones = [
    [41.8781, -87.6298, "Загрязнение городов (Чикаго, США)"],
    [-3.4653, -62.2159, "Вырубка лесов (Амазония)"],
    [30.5728, 104.0668, "Смог и загрязнение воздуха (Китай)"],
    [30, -140, "Пластиковое пятно в Тихом океане"],
    [64.2008, -149.4937, "Таяние льдов (Аляска)"],
    [-18.2871, 147.6992, "Обесцвечивание кораллов (Большой Барьерный риф)"],
    [61.5240, 105.3188, "Лесные пожары (Сибирь)"],
    [15.5527, 48.5164, "Опустынивание (Сахара)"],
    [24.8607, 67.0011, "Загрязнение воды (река Инд)"],
    [40.7128, -74.0060, "Загрязнение воздуха (Нью-Йорк)"],
    [-4.0383, 21.7587, "Вырубка тропических лесов (Конго)"],
    [-82.8628, 135.0000, "Климатические изменения (Антарктида)"]
];

zones.forEach(z => {
    L.marker([z[0], z[1]]).addTo(map).bindPopup(z[2]);
});
</script>

</body>
</html>

<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Сохранение экологии</title>

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

header h1 { margin: 0; font-size: 36px; }

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

body.dark .toggle { background: #333; color: white; }

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
    transition: 0.8s ease;
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

h2 { color: var(--accent); }
</style>
</head>

<body>

<header>
    <button class="toggle" onclick="toggleTheme()">🌙 Тема</button>
    <h1>Сохранение экологии</h1>
    <p>Наш вклад в чистое и безопасное будущее планеты</p>
</header>

<nav>
    <a href="#eco">Экология</a>
    <a href="#problems">Проблемы</a>
    <a href="#tasks">Задачи</a>
    <a href="#mapSection">Карта</a>
</nav>

<section id="eco">
<div class="card">
<h2>Что такое экология?</h2>
<p>Экология — наука о взаимодействии живых организмов и среды.</p>
</div>
</section>

<section id="problems">
<div class="card">
<h2>Проблемы</h2>
<ul>
<li>Загрязнение воздуха</li>
<li>Вырубка лесов</li>
<li>Пластик</li>
<li>Глобальное потепление</li>
</ul>
</div>
</section>

<section id="tasks">
<div class="card">
<h2>Задачи</h2>
<ul>
<li>Переработка отходов</li>
<li>Экономия ресурсов</li>
<li>Озеленение</li>
</ul>
</div>
</section>

<section id="mapSection">
<div class="card">
<h2>Экологическая карта</h2>
<div id="map"></div>
</div>
</section>

<footer>
© 2026 Экология
</footer>

<script>
// анимации
const cards = document.querySelectorAll('.card');
const observer = new IntersectionObserver(e=>{
    e.forEach(i=>{
        if(i.isIntersecting) i.target.classList.add('show');
    });
},{threshold:0.2});
cards.forEach(c=>observer.observe(c));

// тема
function toggleTheme(){
    document.body.classList.toggle('dark');
}

// карта
var map = L.map('map').setView([20,0],2);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',{
    attribution:'© OpenStreetMap'
}).addTo(map);

// точки
const zones = [
    [41.87,-87.62,"Чикаго"],
    [-3.46,-62.21,"Амазония"],
    [30.57,104.06,"Китай смог"],
    [64.2,-149.49,"Аляска"],
    [-18.28,147.7,"Большой Барьерный риф"],
    [61.52,105.31,"Сибирь пожары"],
    [15.55,48.51,"Сахара"],
    [24.86,67.00,"Инд"],
    [40.71,-74.00,"Нью-Йорк"],
    [-4.03,21.75,"Конго"],
    [-82.86,135.0,"Антарктида"]
];

zones.forEach(z=>{
    L.marker([z[0],z[1]]).addTo(map).bindPopup(z[2]);
});
</script>

</body>
</html>

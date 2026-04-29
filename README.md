# Monster-<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8" />

<meta name="viewport" content="width=device-width, initial-scale=1.0"/>

<title>Monster Mode Fitness</title>

<style>

body {

    margin: 0;

    font-family: Arial, sans-serif;

    background: #0b0f0a;

    color: #00ff66;

    text-align: center;

}

header {

    padding: 20px;

    font-size: 28px;

    font-weight: bold;

    text-shadow: 0 0 10px #00ff66;

}

.card {

    background: #111;

    margin: 15px;

    padding: 15px;

    border-radius: 12px;

    box-shadow: 0 0 10px #00ff66;

}

button {

    background: #00ff66;

    border: none;

    padding: 10px 15px;

    margin: 5px;

    border-radius: 8px;

    cursor: pointer;

    font-weight: bold;

}

button:hover {

    background: #00cc55;

}

.progress {

    width: 80%;

    height: 20px;

    background: #222;

    margin: 10px auto;

    border-radius: 10px;

    overflow: hidden;

}

.bar {

    height: 100%;

    width: 0%;

    background: #00ff66;

    transition: 0.5s;

}

.small {

    font-size: 14px;

    color: #aaa;

}

</style>

</head>

<body>

<header>👾 MONSTER MODE FITNESS 👾</header>

<div class="card">

    <h2>Level: <span id="level">1</span></h2>

    <h3>XP: <span id="xp">0</span> / 100</h3>

    <div class="progress"><div class="bar" id="bar"></div></div>

</div>

<div class="card">

    <h2>🔥 Daily Monster Quest</h2>

    <p id="quest">Click below to get your mission</p>

    <button onclick="newQuest()">Generate Quest</button>

    <button onclick="completeQuest()">Complete Quest (+20 XP)</button>

</div>

<div class="card">

    <h2>💧 Daily Habits</h2>

    <p class="small">Simple habits = faster progress (no extreme dieting)</p>

    <button onclick="toggleHabit('water')">Drink Water</button>

    <button onclick="toggleHabit('steps')">Move / Walk</button>

    <button onclick="toggleHabit('sleep')">Good Sleep</button>

    <p id="habits">None completed yet</p>

</div>

<script>

let xp = localStorage.getItem("xp") ? parseInt(localStorage.getItem("xp")) : 0;

let level = localStorage.getItem("level") ? parseInt(localStorage.getItem("level")) : 1;

function updateUI() {

    document.getElementById("xp").innerText = xp;

    document.getElementById("level").innerText = level;

    let percent = (xp % 100);

    document.getElementById("bar").style.width = percent + "%";

}

function addXP(amount) {

    xp += amount;

    if (xp >= level * 100) {

        level++;

    }

    localStorage.setItem("xp", xp);

    localStorage.setItem("level", level);

    updateUI();

}

function newQuest() {

    const quests = [

        "Do 20 squats 👹",

        "Do 10 push-ups 👊",

        "1 min plank challenge 🧱",

        "30 jumping jacks ⚡",

        "Walk for 10–15 minutes 🚶",

        "Shadow boxing for 2 minutes 🥊"

    ];

    let q = quests[Math.floor(Math.random() * quests.length)];

    document.getElementById("quest").innerText = q;

}

function completeQuest() {

    addXP(20);

}

let habits = {

    water: false,

    steps: false,

    sleep: false

};

function toggleHabit(h) {

    habits[h] = true;

    updateHabits();

    addXP(10);

}

function updateHabits() {

    let done = Object.keys(habits).filter(k => habits[k]);

    document.getElementById("habits").innerText =

        done.length ? "Completed: " + done.join(", ") : "None completed yet";

}

updateUI();

updateHabits();

</script>

</body>

</html>

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Aventura no Intestino Delgado</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="game-container">
        <h1>A Aventura no Intestino Delgado</h1>
        <div id="level">Nível: 1</div>
        <div id="score">Pontos: 0</div>
        <div id="questions-container"></div>
        <div id="nutrients-container"></div>
        <button id="start-btn">Iniciar</button>
    </div>
    <script src="script.js"></script>
</body>
</html>

body {
    font-family: Arial, sans-serif;
    background-color: #f2f2f2;
}

#game-container {
    text-align: center;
    margin: 20px auto;
    max-width: 600px;
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

#nutrients-container {
    margin: 20px 0;
}

.nutrient {
    display: inline-block;
    margin: 5px;
    padding: 10px;
    background-color: #4caf50;
    color: white;
    border-radius: 5px;
    animation: bounce 0.5s;
}

@keyframes bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
}
let score = 0;
let level = 1;
const nutrients = ['Carboidratos', 'Proteínas', 'Lipídios'];
const questions = [
    { question: "Qual é a função do duodeno?", answer: "Quebrar alimentos com enzimas" },
    { question: "O jejuno é responsável por?", answer: "Absorver nutrientes" },
    { question: "O íleo ajuda na?", answer: "Absorção de vitaminas" },
];

document.getElementById('start-btn').addEventListener('click', startGame);

function startGame() {
    score = 0;
    level = 1;
    document.getElementById('level').innerText = `Nível: ${level}`;
    document.getElementById('score').innerText = `Pontos: ${score}`;
    document.getElementById('nutrients-container').innerHTML = '';
    askQuestion();
}

function askQuestion() {
    const questionIndex = Math.floor(Math.random() * questions.length);
    const question = questions[questionIndex];

    const userAnswer = prompt(question.question);
    if (userAnswer && userAnswer.toLowerCase() === question.answer.toLowerCase()) {
        score += 10;
        document.getElementById('score').innerText = `Pontos: ${score}`;
        collectNutrient();
    } else {
        alert("Resposta incorreta. Tente novamente!");
    }

    if (score >= 30 * level) {
        level++;
        document.getElementById('level').innerText = `Nível: ${level}`;
        alert("Parabéns! Você avançou para o próximo nível!");
    }

    if (level <= 3) {
        askQuestion(); // Chama nova pergunta se ainda houver níveis
    } else {
        alert("Você completou todos os níveis! Pontuação final: " + score);
        // Aqui poderia reiniciar ou mostrar a tela de fim de jogo
    }
}

function collectNutrient() {
    const nutrient = nutrients[Math.floor(Math.random() * nutrients.length)];
    const nutrientDiv = document.createElement('div');
    nutrientDiv.classList.add('nutrient');
    nutrientDiv.innerText = nutrient;
    document.getElementById('nutrients-container').appendChild(nutrientDiv);
}
<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
function setup() {
    createCanvas(400, 200);
    background(200);
}

function draw() {
    fill(255, 0, 0);
    ellipse(50, 50, 50, 50); // Exemplo de círculo
}

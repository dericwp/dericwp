<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Petualangan Empati</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div id="main-menu">
    <h1>Petualangan Empati</h1>
    <button id="start-button">Mulai</button>
  </div>

  <div id="game-screen" style="display: none;">
    <h2 id="question-title"></h2>
    <img id="question-image" src="" alt="Gambar Pertanyaan">
    <div id="options-container"></div>
  </div>

  <div id="score-screen" style="display: none;">
    <h1>Skor Anda</h1>
    <p id="final-score"></p>
    <button id="restart-button">Main Lagi</button>
  </div>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f0f8ff;
  margin: 0;
  padding: 0;
}

#main-menu, #game-screen, #score-screen {
  padding: 20px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

#question-image {
  max-width: 300px;
  margin: 20px auto;
}
let currentQuestionIndex = 0;
let score = 0;

const questions = [
  {
    title: "Apa emosi yang terlihat di gambar ini?",
    image: "assets/images/happy.png", // Gambar ilustrasi ekspresi
    options: ["Senang", "Sedih", "Marah", "Takut"],
    answer: "Senang"
  },
  {
    title: "Mengapa Mimi dan adiknya bertengkar?",
    image: "assets/images/story.png", // Gambar cerita
    options: ["Berebut mainan", "Bosan", "Ingin tidur"],
    answer: "Berebut mainan"
  },
  {
    title: "Apa tindakan yang paling tepat untuk Mimi?",
    image: "assets/images/fix.png", // Ilustrasi konflik selesai
    options: ["Meminta maaf", "Diam saja", "Marah balik"],
    answer: "Meminta maaf"
  }
];

document.getElementById("start-button").addEventListener("click", () => {
  document.getElementById("main-menu").style.display = "none";
  document.getElementById("game-screen").style.display = "block";
  showQuestion();
});

function showQuestion() {
  if (currentQuestionIndex < questions.length) {
    const question = questions[currentQuestionIndex];
    document.getElementById("question-title").textContent = question.title;
    document.getElementById("question-image").src = question.image;
    const optionsContainer = document.getElementById("options-container");
    optionsContainer.innerHTML = "";

    question.options.forEach(option => {
      const button = document.createElement("button");
      button.textContent = option;
      button.addEventListener("click", () => checkAnswer(option));
      optionsContainer.appendChild(button);
    });
  } else {
    endGame();
  }
}

function checkAnswer(selectedOption) {
  const correctAnswer = questions[currentQuestionIndex].answer;
  if (selectedOption === correctAnswer) {
    score += 10;
  }
  currentQuestionIndex++;
  showQuestion();
}

function endGame() {
  document.getElementById("game-screen").style.display = "none";
  document.getElementById("score-screen").style.display = "block";
  document.getElementById("final-score").textContent = `Skor Anda: ${score}`;
}

document.getElementById("restart-button").addEventListener("click", () => {
  currentQuestionIndex = 0;
  score = 0;
  document.getElementById("score-screen").style.display = "none";
  document.getElementById("main-menu").style.display = "block";
});

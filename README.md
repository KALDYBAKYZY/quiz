Documentation for "Quiz Game with Images" Project
Project Description
"Quiz Game with Images" is a web-based application that presents a quiz with questions where the answers are provided in the form of images. Users select one of the offered options, and the system checks the correctness of the answer. At the end of the game, the overall result is displayed.
Key Features
1.	Displaying questions with answer choices in image format.
2.	Highlighting the correct and incorrect answers after selection.
3.	Scoring points for correct answers.
4.	"Restart Quiz" button for starting the game over.
5.	Cross-browser responsive design.
Project File Structure
HTML: final.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz Game with Images</title>
  <link rel="stylesheet" href="style2.css">
</head>
<body>
  <div id="quiz-container">
    <h1>Quiz Game</h1>
    <div id="question-container">
      <p id="question"></p>
      <div id="choices-container"></div>
    </div>
    <div id="button-container">
      <button id="next-button" disabled>Next</button>
      <button id="restart-button" style="display:none;">Restart Quiz</button>
    </div>
    <div id="score-container"></div>
  </div>
  <script src="script2.js"></script>
</body>
</html>
CSS: style2.css
body {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
  font-family: Arial, sans-serif;
  text-align: center;
  background-image: url('фон.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  padding: 0;
}

#quiz-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 900px;
  height: 450px;
  max-width: 700px;
  padding: 20px;
  background-color: #fff;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
  border-radius: 8px;
}

h1 {
  color: #2c2c2c;
  font-size: 45px;
}

#question {
  font-size: 1.2rem;
  margin-bottom: 20px;
}

#choices-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
}

.choice-image {
  width: 160px;
  height: 160px;
  border: 3px solid transparent;
  border-radius: 8px;
  cursor: pointer;
  transition: transform 0.3s, border-color 0.3s;
}

.choice-image:hover {
  transform: scale(1.1);
}

.choice-image.correct {
  border-color: #28a745;
}

.choice-image.incorrect {
  border-color: #dc3545;
}

#button-container {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 20px;
}

#next-button {
  padding: 10px 20px;
  font-size: 1rem;
  background-color: #ffc800;
  color: #000000;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

#next-button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

#restart-button {
  border-radius: 5px;
  background-color: #ffa200;
  color: black;
  padding: 7px;
  font-size: 20px;
  cursor: pointer;
  transition: background-color 0.3s;
  border: none;
}
JavaScript: script2.js
const quizQuestions = [
    {
      question: "Which of these is the Eiffel Tower?",
      choices: [
        "биг бен.jpeg",
        "будж халифа.jpeg",
        "эйфеловая башня.jpeg",
        "пизанская.jpeg"
      ],
      correctAnswer: 2
    },
    {
      question: "Identify the Colosseum in Rome.",
      choices: [
        "базилика.avif",
        "коллезей.webp",
        "римский форум.webp",
        "пирамида.jpeg"
      ],
      correctAnswer: 1
    }
];

let currentQuestionIndex = 0;
let score = 0;
const questionElement = document.getElementById("question");
const choicesContainer = document.getElementById("choices-container");
const nextButton = document.getElementById("next-button");

function loadQuestion() {
  const currentQuestion = quizQuestions[currentQuestionIndex];
  questionElement.textContent = currentQuestion.question;

  choicesContainer.innerHTML = "";
  currentQuestion.choices.forEach((imageUrl, index) => {
    const img = document.createElement("img");
    img.src = imageUrl;
    img.classList.add("choice-image");
    img.addEventListener("click", () => handleChoiceClick(index));
    choicesContainer.appendChild(img);
  });
  nextButton.disabled = true;
}

function handleChoiceClick(selectedIndex) {
  const currentQuestion = quizQuestions[currentQuestionIndex];
  const choiceImages = document.querySelectorAll(".choice-image");
  choiceImages.forEach((img) => (img.style.pointerEvents = "none"));
  if (selectedIndex === currentQuestion.correctAnswer) {
    score++;
    choiceImages[selectedIndex].classList.add("correct");
  } else {
    choiceImages[selectedIndex].classList.add("incorrect");
    choiceImages[currentQuestion.correctAnswer].classList.add("correct");
  }

  nextButton.disabled = false;
}

function showScore() {
  questionElement.textContent = "Quiz Complete!";
  choicesContainer.innerHTML = `
  <div style="display: flex; flex-direction: column; align-items: center;">
      <p style="font-size: 20px; text-align: center;">Your score is ${score} out of ${quizQuestions.length} 🎉</p>
      <button id="restart-button" style="margin-top: 20px;">Restart Quiz</button>
  </div>`;

  const restartButton = document.getElementById("restart-button");
  restartButton.addEventListener("click", restartQuiz);

  nextButton.style.display = "none";
}

function restartQuiz() {
  currentQuestionIndex = 0;
  score = 0;
  nextButton.style.display = "block";
  loadQuestion();
}

nextButton.addEventListener("click", () => {
  currentQuestionIndex++;
  if (currentQuestionIndex < quizQuestions.length) {
    loadQuestion();
  } else {
    showScore();
  }
});
loadQuestion();
Installation and Setup
1.	Clone the repository or download the files.
2.	Place all files in a single directory.
3.	Open index.html in your browser to start the quiz game
File Structure

quiz-project/
├── index.html
├── style2.css
├── script2.js
├── images

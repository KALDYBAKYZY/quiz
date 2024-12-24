<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz Game with Images</title>
  <!-- Подключение внешнего файла стилей -->
  <link rel="stylesheet" href="style2.css">
</head>
<body>
  <!-- Основной контейнер викторины -->
  <div id="quiz-container">
    <!-- Заголовок игры -->
    <h1>Quiz Game</h1>

    <!-- Контейнер для отображения вопроса и вариантов ответа -->
    <div id="question-container">
      <p id="question"></p> <!-- Здесь будет отображаться текст вопроса -->
      <div id="choices-container"></div> <!-- Контейнер для вариантов ответа -->
    </div>

    <!-- Контейнер для кнопок -->
    <div id="button-container">
      <!-- Кнопка перехода к следующему вопросу -->
      <button id="next-button" disabled>Next</button>
      <!-- Кнопка перезапуска игры (по умолчанию скрыта) -->
      <button id="restart-button" style="display:none;">Restart Quiz</button>
    </div>

    <!-- Контейнер для отображения итогового результата -->
    <div id="score-container"></div>
  </div>

  <!-- Подключение файла со скриптами -->
  <script src="script2.js"></script>
</body>
</html>
body {
  /* Установка flexbox для центрирования содержимого */
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Высота окна браузера */
  margin: 0; /* Убираем внешние отступы */
  font-family: Arial, sans-serif; /* Шрифт для текста */
  text-align: center; /* Центрирование текста */
  background-image: url('/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/фон.jpg'); /* Фоновое изображение */
  background-repeat: no-repeat; /* Запрет на повтор изображения */
  background-size: cover; /* Масштабирование изображения для покрытия всего экрана */
  padding: 0; /* Убираем внутренние отступы */
}

#quiz-container {
  /* Центрирование контейнера относительно страницы */
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%); /* Перемещение в центр */
  width: 900px; /* Ширина контейнера */
  height: 450px; /* Высота контейнера */
  max-width: 700px; /* Максимальная ширина для адаптивности */
  padding: 20px; /* Внутренние отступы */
  background-color: #fff; /* Белый фон */
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1); /* Тень для объёма */
  border-radius: 8px; /* Скругление углов */
}

h1 {
  color: #2c2c2c; /* Цвет текста */
  font-size: 45px; /* Размер шрифта заголовка */
}

#question {
  font-size: 1.2rem; /* Размер текста вопроса */
  margin-bottom: 20px; /* Отступ снизу */
}

#choices-container {
  /* Упорядочивание вариантов ответов */
  display: flex;
  flex-wrap: wrap; /* Перенос строк, если вариантов больше */
  justify-content: center; /* Центрирование содержимого */
  gap: 10px; /* Отступы между элементами */
}

.choice-image {
  /* Стили для изображений выбора */
  width: 160px; /* Ширина изображений */
  height: 160px; /* Высота изображений */
  border: 3px solid transparent; /* Прозрачная рамка по умолчанию */
  border-radius: 8px; /* Скругление углов */
  cursor: pointer; /* Указатель мыши при наведении */
  transition: transform 0.3s, border-color 0.3s; /* Анимация при наведении */
}

.choice-image:hover {
  /* Анимация увеличения изображения при наведении */
  transform: scale(1.1);
}

.choice-image.correct {
  border-color: #28a745; /* Зелёная рамка для правильного ответа */
}

.choice-image.incorrect {
  border-color: #dc3545; /* Красная рамка для неправильного ответа */
}

#button-container {
  /* Контейнер для кнопок */
  display: flex;
  justify-content: center; /* Центрирование кнопок */
  gap: 10px; /* Расстояние между кнопками */
  margin-top: 20px; /* Отступ сверху */
}

#next-button {
  /* Стили для кнопки "Далее" */
  padding: 10px 20px; /* Внутренние отступы */
  font-size: 1rem; /* Размер шрифта */
  background-color: #ffc800; /* Жёлтый фон */
  color: #000000; /* Чёрный текст */
  border: none; /* Без рамки */
  border-radius: 5px; /* Скругление углов */
  cursor: pointer; /* Указатель мыши */
  transition: background-color 0.3s; /* Анимация при изменении цвета */
}

#next-button:disabled {
  background-color: #ccc; /* Серый цвет для неактивной кнопки */
  cursor: not-allowed; /* Запретный указатель мыши */
}

#restart-button {
  /* Стили для кнопки "Начать заново" */
  border-radius: 5px; /* Скругление углов */
  background-color: #ffa200; /* Оранжевый фон */
  color: black; /* Чёрный текст */
  padding: 7px; /* Внутренние отступы */
  font-size: 20px; /* Размер шрифта */
  cursor: pointer; /* Указатель мыши */
  transition: background-color 0.3s; /* Анимация при изменении цвета */
  border: none; /* Без рамки */
}
const quizQuestions = [
    {
      question: "Which of these is the Eiffel Tower?",
      choices: [
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/биг бен.jpeg", 
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/будж халифа.jpeg",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/эйфеловая башня.jpeg",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/пизанская.jpeg"
      ],
      correctAnswer: 2
    },
    {
      question: "Identify the Colosseum in Rome.",
      choices: [
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/базилика.avif",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/коллезей.webp", 
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/римский форум.webp",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/пирамида.jpeg"
      ],
      correctAnswer: 1
    },
    {
      question: "Where is the park of the first president.",
      choices: [
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/кок тобе.jpeg",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/медеу.jpeg", 
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/парк первого .jpeg",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/парк горького.jpeg"
      ],
      correctAnswer: 2
    },
    {
      question: "Monument located in the capital of Kazakhstan.",
      choices: [
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/байтерек.jpeg",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/красная площадб.jpeg", 
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/хан шатыр.jpeg",
        "/Users/gulnazzhaiylgan/Library/Mobile Documents/com~apple~CloudDocs/html/final1/будж халифа.jpeg"
      ],
      correctAnswer: 0
    }
  ];
  
  let currentQuestionIndex = 0; // Индекс текущего вопроса
  let score = 0; // Счёт игрока
  
  // Ссылки на элементы DOM
  const questionElement = document.getElementById("question");
  const choicesContainer = document.getElementById("choices-container");
  const nextButton = document.getElementById("next-button");
  const scoreContainer = document.getElementById("score-container");
  
  function loadQuestion() {
    /* Функция загрузки текущего вопроса */
    const currentQuestion = quizQuestions[currentQuestionIndex]; // Текущий вопрос
    questionElement.textContent = currentQuestion.question; // Отображение текста вопроса
  
    choicesContainer.innerHTML = ""; // Очистка контейнера вариантов ответа
    currentQuestion.choices.forEach((imageUrl, index) => {
        const img = document.createElement("img"); // Создаём элемент <img>
        img.src = imageUrl; // Устанавливаем путь к изображению
        img.classList.add("choice-image"); // Добавляем CSS-класс
        img.addEventListener("click", () => handleChoiceClick(index)); // Назначаем обработчик клика
        choicesContainer.appendChild(img); // Добавляем изображение в контейнер
    });
  
    nextButton.disabled = true; // Отключаем кнопку "Далее", пока не выбран ответ
  }
  
  function handleChoiceClick(selectedIndex) {
    /* Обработчик клика по варианту ответа */
    const currentQuestion = quizQuestions[currentQuestionIndex];
    const choiceImages = document.querySelectorAll(".choice-image");
    choiceImages.forEach((img) => (img.style.pointerEvents = "none")); // Отключаем взаимодействие с вариантами
  
    if (selectedIndex === currentQuestion.correctAnswer) {
        // Если выбран правильный ответ
        score++; // Увеличиваем счёт
        choiceImages[selectedIndex].classList.add("correct"); // Добавляем класс "правильный"
    } else {
        // Если выбран неправильный ответ
        choiceImages[selectedIndex].classList.add("incorrect"); // Добавляем класс "неправильный"
        choiceImages[currentQuestion.correctAnswer].classList.add("correct"); // Подсвечиваем правильный ответ
    }
  
    nextButton.disabled = false; // Включаем кнопку "Далее"
  }
  
  function showScore() {
    /* Функция отображения результата */
    questionElement.textContent = "Quiz Complete!"; // Заголовок результата
    choicesContainer.innerHTML = `
        <div style="display: flex; flex-direction: column; align-items: center;">
            <p style="font-size: 20px; text-align: center;">Your score is ${score} out of ${quizQuestions.length} 🎉</p>
            <button id="restart-button" style="margin-top: 20px;">Restart Quiz</button>
        </div>`;
    // Кнопка перезапуска
    const restartButton = document.getElementById("restart-button");
    restartButton.addEventListener("click", restartQuiz); // Назначаем обработчик
  
    nextButton.style.display = "none"; // Скрываем кнопку "Далее"
  }
  
  function restartQuiz() {
    /* Функция перезапуска викторины */
    currentQuestionIndex = 0; // Сброс индекса
    score = 0; // Сброс счёта
    nextButton.style.display = "block"; // Показываем кнопку "Далее"
    loadQuestion(); // Загружаем первый вопрос
  }
  
  // Обработчик клика по кнопке "Далее"
  nextButton.addEventListener("click", () => {
    currentQuestionIndex++; // Переход к следующему вопросу
    if (currentQuestionIndex < quizQuestions.length) {
        loadQuestion(); // Загрузка следующего вопроса
    } else {
        showScore(); // Если вопросов больше нет, показываем результат
    }
  });
  
  // Инициализация первого вопроса
  loadQuestion();

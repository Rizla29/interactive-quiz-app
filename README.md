<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Interactive Quiz Application</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #f4f7fa;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
    }
    .quiz-container {
      background: #fff;
      padding: 30px;
      border-radius: 15px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.1);
      width: 400px;
      max-width: 90%;
    }
    h1 {
      text-align: center;
      color: #6a0dad;
      margin-bottom: 25px;
    }
    h2 {
      color: #333;
      margin-bottom: 15px;
    }
    .btn {
      background-color: #4a90e2;
      color: white;
      border: none;
      padding: 10px;
      margin: 5px 0;
      border-radius: 6px;
      width: 100%;
      cursor: pointer;
      transition: background 0.3s;
    }
    .btn:hover {
      background-color: #357ab7;
    }
    #submit {
      background-color: white;
      color: #6a0dad;
      border: 2px solid #6a0dad;
      font-weight: bold;
      margin-top: 15px;
    }
    #submit:hover {
      background-color: #6a0dad;
      color: white;
    }
    .result {
      margin-top: 20px;
      text-align: center;
      font-size: 1.1rem;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>Interactive Quiz Application</h1>
    <h2 id="question">Loading question...</h2>
    <div id="options"></div>
    <button id="submit" class="btn">Submit Answer</button>
    <div class="result" id="result"></div>
  </div>

  <script>
    const quizData = [
      {
        question: "1. What does HTML stand for?",
        options: [
          "Hyper Trainer Marking Language",
          "Hyper Text Markup Language",
          "Hyper Text Marketing Language",
          "Hyper Text Markdown Language"
        ],
        answer: "Hyper Text Markup Language"
      },
      {
        question: "2. Which tag is used to create a hyperlink in HTML?",
        options: ["<img>", "<a>", "<link>", "<href>"],
        answer: "<a>"
      },
      {
        question: "3. What does CSS stand for?",
        options: [
          "Cascading Style Sheets",
          "Creative Style Syntax",
          "Computer Style Sheet",
          "Colorful Style Sheet"
        ],
        answer: "Cascading Style Sheets"
      },
      {
        question: "4. Which property is used to change the background color in CSS?",
        options: ["color", "background", "background-color", "bgcolor"],
        answer: "background-color"
      },
      {
        question: "5. Which HTML tag is used to insert an image?",
        options: ["<image>", "<img>", "<pic>", "<src>"],
        answer: "<img>"
      },
      {
        question: "6. How do you center text using CSS?",
        options: [
          "text-align: center;",
          "align-text: center;",
          "center-text: true;",
          "text: center;"
        ],
        answer: "text-align: center;"
      }
    ];

    let currentQuestion = 0;
    let score = 0;
    let selectedAnswer = "";

    const questionEl = document.getElementById("question");
    const optionsEl = document.getElementById("options");
    const resultEl = document.getElementById("result");
    const submitBtn = document.getElementById("submit");

    function loadQuestion() {
      const q = quizData[currentQuestion];
      questionEl.innerText = q.question;
      optionsEl.innerHTML = "";
      selectedAnswer = "";

      q.options.forEach(option => {
        const btn = document.createElement("button");
        btn.classList.add("btn");
        btn.innerText = option;
        btn.onclick = () => selectOption(btn, option);
        optionsEl.appendChild(btn);
      });
    }

    function selectOption(button, option) {
      const allBtns = document.querySelectorAll(".btn");
      allBtns.forEach(btn => {
        if (btn !== submitBtn) btn.style.backgroundColor = "#4a90e2";
      });
      button.style.backgroundColor = "#2a2a72";
      selectedAnswer = option;
    }

    submitBtn.addEventListener("click", () => {
      if (!selectedAnswer) {
        alert("Please select an answer!");
        return;
      }

      const correctAnswer = quizData[currentQuestion].answer;
      resultEl.innerText =
        selectedAnswer === correctAnswer
          ? "✅ Correct!"
          : `❌ Wrong! Correct answer: ${correctAnswer}`;
      resultEl.style.color = selectedAnswer === correctAnswer ? "green" : "red";

      if (selectedAnswer === correctAnswer) score++;

      setTimeout(() => {
        currentQuestion++;
        resultEl.innerText = "";

        if (currentQuestion < quizData.length) {
          loadQuestion();
        } else {
          endQuiz();
        }
      }, 1000);
    });

    function endQuiz() {
      questionEl.innerText = "🎉 Quiz Completed!";
      optionsEl.innerHTML = `<p>Your Final Score: ${score} / ${quizData.length}</p>`;
      submitBtn.style.display = "none";
    }

    // Load first question
    loadQuestion();
  </script>
</body>
</html>


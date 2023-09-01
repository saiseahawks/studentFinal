---
toc: true
title: Python IO
comments: true
layout: post
description: A Quick Quiz on Python
courses: { compsci: {week: 2} }
type: hacks
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Quiz</title>
</head>
<body>
  <h1>Interactive Quiz</h1>
  <div id="question"></div>
  <div id="response"></div>
  <script>
    const questions = [
      {
        question: "What command is used to include other functions that were previously developed?",
        correctAnswer: "import"
      },
      {
        question: "What command is used to evaluate correct or incorrect response in this example?",
        correctAnswer: "if"
      },
      {
        question: "Each 'if' command contains an '_________' to determine a true or false condition?",
        correctAnswer: "expression"
      }
    ];

    let currentQuestion = 0;
    let correct = 0;

    function displayQuestion() {
      const questionDiv = document.getElementById("question");
      const responseDiv = document.getElementById("response");
      responseDiv.innerHTML = "";
      
      if (currentQuestion < questions.length) {
        const question = questions[currentQuestion].question;
        questionDiv.textContent = "Question: " + question;
        
        const answerButton = document.createElement("button");
        answerButton.textContent = "Submit Answer";
        answerButton.addEventListener("click", checkAnswer);
        responseDiv.appendChild(answerButton);
      } else {
        questionDiv.textContent = "Quiz Completed!";
        responseDiv.textContent = "You scored " + correct + " out of " + questions.length;
      }
    }

    function checkAnswer() {
      const responseDiv = document.getElementById("response");
      const userAnswer = prompt("Your answer:");
      const correctAnswer = questions[currentQuestion].correctAnswer.toLowerCase();
      
      if (userAnswer.toLowerCase() === correctAnswer) {
        responseDiv.textContent = "Correct!";
        correct++;
      } else {
        responseDiv.textContent = "Incorrect. The correct answer is: " + questions[currentQuestion].correctAnswer;
      }
      
      currentQuestion++;
      displayQuestion();
    }

    displayQuestion();
  </script>
</body>
</html>

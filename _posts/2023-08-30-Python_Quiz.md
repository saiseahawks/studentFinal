---
toc: true
title: Python IO
comments: true
layout: post
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
courses: { compsci: {week: 2} }
type: hacks
---
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz</title>
</head>
<body>
  <h1>Quiz Time</h1>
  <p id="output"></p>
  <script>
    const outputElement = document.getElementById("output");
    const questions = 3;
    let correct = 0;

    function questionWithResponse(prompt, callback) {
      const response = prompt(prompt + "\n");
      callback(response);
    }

    questionWithResponse("Are you ready to take a test?", function (response) {
      response = response.toLowerCase();
      if (response === "yes" || response === "y") {
        askQuestion1();
      } else {
        outputElement.textContent = "Test cancelled.";
      }
    });

    function askQuestion1() {
      questionWithResponse("What command is used to include other functions that were previously developed?", function (response) {
        response = response.toLowerCase();
        if (response === "import") {
          outputElement.textContent = response + " is correct!";
          correct++;
        } else {
          outputElement.textContent = response + " is incorrect!";
        }
        askQuestion2();
      });
    }

    function askQuestion2() {
      questionWithResponse("What command is used to evaluate correct or incorrect response in this example?", function (response) {
        response = response.toLowerCase();
        if (response === "if") {
          outputElement.textContent = response + " is correct!";
          correct++;
        } else {
          outputElement.textContent = response + " is incorrect!";
        }
        askQuestion3();
      });
    }

    function askQuestion3() {
      questionWithResponse("Each 'if' command contains an '_________' to determine a true or false condition?", function (response) {
        response = response.toLowerCase();
        if (response === "expression") {
          outputElement.textContent = response + " is correct!";
          correct++;
        } else {
          outputElement.textContent = response + " is incorrect!";
        }
        displayScore();
      });
    }

    function displayScore() {
      outputElement.textContent = "You scored " + correct + "/" + questions;
    }
  </script>
</body>
</html>

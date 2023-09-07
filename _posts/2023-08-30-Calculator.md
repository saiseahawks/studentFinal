---
toc: true
title: JS Calculator
comments: true
layout: post
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
courses: { compsci: {week: 2} }
type: hacks
---
<style>
  body {
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background-color: #f0f0f0;
  }

  .calculator-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    max-width: 400px;
    background-color: #fff;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .calculator-output {
    grid-column: span 4;
    border-radius: 10px;
    padding: 0.5em;
    font-size: 24px;
    border: 2px solid #333;
    text-align: right;
    background-color: #f8f8f8;
  }

  .calculator-button {
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 20px;
    height: 60px;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.3s, color 0.3s;
  }

  .calculator-number {
    background-color: #f0f0f0;
  }

  .calculator-operation {
    background-color: #f8c471;
  }

  .calculator-clear {
    background-color: #e74c3c;
    color: #fff;
  }

  .calculator-equals {
    background-color: #2ecc71;
    color: #fff;
  }

  .calculator-button:hover {
    background-color: #ddd;
  }
</style>

<!-- Add a container for the animation -->
<div id="animation">
  <div class="calculator-container">
    <!--result-->
    <div class="calculator-output" id="output">0</div>
    <!--row 1 to 4-->
    <div class="calculator-button calculator-number">1</div>
    <div class="calculator-button calculator-number">2</div>
    <div class="calculator-button calculator-number">3</div>
    <div class="calculator-button calculator-operation">+</div>
    <div class="calculator-button calculator-number">4</div>
    <div class="calculator-button calculator-number">5</div>
    <div class="calculator-button calculator-number">6</div>
    <div class="calculator-button calculator-operation">-</div>
    <div class="calculator-button calculator-number">7</div>
    <div class="calculator-button calculator-number">8</div>
    <div class="calculator-button calculator-number">9</div>
    <div class="calculator-button calculator-operation">*</div>
    <div class="calculator-button calculator-clear">A/C</div>
    <div class="calculator-button calculator-number">0</div>
    <div class="calculator-button calculator-number">.</div>
    <div class="calculator-button calculator-equals">=</div>
  </div>
</div>

<!-- JavaScript and animation scripts -->
<script>
  // initialize important variables to manage calculations
var firstNumber = null;
var operator = null;
var nextReady = true;

// build objects containing key elements
const output = document.getElementById("output");
const numbers = document.querySelectorAll(".calculator-number");
const operations = document.querySelectorAll(".calculator-operation");
const clear = document.querySelectorAll(".calculator-clear");
const equals = document.querySelectorAll(".calculator-equals");

// Number buttons listener
numbers.forEach(button => {
  button.addEventListener("click", function() {
    number(button.textContent);
  });
});

// Number action
function number(value) {
  if (value != ".") {
    if (nextReady == true) {
      output.innerHTML = value;
      if (value != "0") {
        nextReady = false;
      }
    } else {
      output.innerHTML = output.innerHTML + value;
    }
  } else {
    if (output.innerHTML.indexOf(".") == -1) {
      output.innerHTML = output.innerHTML + value;
      nextReady = false;
    }
  }
}

// Operation buttons listener
operations.forEach(button => {
  button.addEventListener("click", function() {
    operation(button.textContent);
  });
});

// Operator action
function operation(choice) {
  if (firstNumber == null) {
    firstNumber = parseInt(output.innerHTML);
    nextReady = true;
    operator = choice;
    return;
  }
  firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
  operator = choice;
  output.innerHTML = firstNumber.toString();
  nextReady = true;
}

// Calculator
function calculate(first, second) {
  let result = 0;
  switch (operator) {
    case "+":
      result = first + second;
      break;
    case "-":
      result = first - second;
      break;
    case "*":
      result = first * second;
      break;
    case "/":
      result = first / second;
      break;
    default:
      break;
  }
  return result;
}

// Equals button listener
equals.forEach(button => {
  button.addEventListener("click", function() {
    equal();
  });
});

// Equal action
function equal() {
  firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
  output.innerHTML = firstNumber.toString();
  nextReady = true;
}

// Clear button listener
clear.forEach(button => {
  button.addEventListener("click", function() {
    clearCalc();
  });
});

// A/C action
function clearCalc() {
  firstNumber = null;
  output.innerHTML = "0";
  nextReady = true;
}

</script>

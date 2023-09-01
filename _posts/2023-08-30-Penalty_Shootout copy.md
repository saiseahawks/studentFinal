---
toc: true
title: Classic Soccer Game
layout: post
description: Fun highly challenging guessing game
courses: {compsci: {week: 2}}
type: hacks
---
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Football Penalty Shootout Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            text-align: center;
            padding: 20px;
            background-color: #fff;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        h1 {
            margin-bottom: 20px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background-color: #0056b3;
        }

        #gameOutput {
            margin-top: 20px;
            text-align: left;
        }

        p {
            margin: 10px 0;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Welcome to the Football Penalty Shootout Game!</h1>
        <button id="startButton">Start Game</button>
        <div id="gameOutput"></div>
    </div>
    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const startButton = document.getElementById("startButton");
            const gameOutput = document.getElementById("gameOutput");
            
            function playGame() {
                gameOutput.innerHTML = "";
                const total_shots = 5;
                let goals = 0;
                let misses = 0;

                async function penaltyKick(isGoalkeeper) {
                    const direction = isGoalkeeper ? "Save" : "Score";
                    const action = isGoalkeeper ? "saving" : "scoring";
                    const choice = await new Promise((resolve) => {
                        const inputElement = document.createElement("input");
                        inputElement.type = "text";
                        inputElement.placeholder = "left, center, or right";
                        gameOutput.innerHTML += `<p>${direction} left, center, or right? </p>`;
                        gameOutput.appendChild(inputElement);
                        inputElement.addEventListener("keyup", (event) => {
                            if (event.key === "Enter") {
                                resolve(inputElement.value.toLowerCase());
                            }
                        });
                    });

                    const randomChoice = ["left", "center", "right"][Math.floor(Math.random() * 3)];

                    if ((isGoalkeeper && choice === randomChoice) || (!isGoalkeeper && choice !== randomChoice)) {
                        gameOutput.innerHTML += `<p>You saved a shot!!! ${randomChoice.toUpperCase()}!</p>`;
                        if (isGoalkeeper) misses++;
                        else goals++;
                    } else {
                        gameOutput.innerHTML += `<p>Opponent makes the shot ${randomChoice.toUpperCase()}!</p>`;
                        if (isGoalkeeper) goals++;
                        else misses++;
                    }

                    gameOutput.innerHTML += `<p>Score: ${goals} goals, ${misses} misses</p>`;
                }

                async function start() {
                    gameOutput.innerHTML = "";
                    for (let i = 0; i < total_shots; i++) {
                        await penaltyKick(true);
                    }

                    gameOutput.innerHTML += "<p>Now you are the penalty kicker!</p>";

                    for (let i = 0; i < total_shots; i++) {
                        await penaltyKick(false);
                    }

                    gameOutput.innerHTML += "<p>Game Over!</p>";
                    gameOutput.innerHTML += `<p>Final Score: ${goals} goals, ${misses} misses</p>`;
                }

                start();
            }
            startButton.addEventListener("click", playGame);
        });
    </script>
</body>
</html>

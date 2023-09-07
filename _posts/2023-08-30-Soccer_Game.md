---
toc: true
title: Soccer Game
layout: post
description: Fun highly challenging guessing game
courses: {compsci: {week: 3}}
type: hacks
---
<!DOCTYPE html>
<html>
<head>
    <title>Penalty Shootout</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
        }

        #gameContainer {
            max-width: 600px;
            margin: 0 auto;
            background-color: #fff;
            border: 1px solid #ccc;
            padding: 20px;
            border-radius: 10px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #007BFF;
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
    <button id="startButton">Start Penalty Shootout</button>
    <div id="gameOutput"></div>

    <script>
        document.addEventListener("DOMContentLoaded", function () {
            const startButton = document.getElementById("startButton");
            const gameOutput = document.getElementById("gameOutput");

            let goalieGoals = 0;
            let kickerGoals = 0;
            let goalkeeperTurns = 0;

            async function penaltyKick(isGoalkeeper) {
                const direction = isGoalkeeper ? "Save" : "Score";
                const action = isGoalkeeper ? "save" : "score";
                const choice = await new Promise((resolve) => {
                    const inputElement = document.createElement("input");
                    inputElement.type = "text";
                    inputElement.placeholder = "left, center, or right";
                    gameOutput.innerHTML += `<p>${direction} left, center, or right?</p>`;
                    gameOutput.appendChild(inputElement);
                    inputElement.addEventListener("keyup", (event) => {
                        if (event.key === "Enter") {
                            resolve(inputElement.value.toLowerCase());
                        }
                    });
                });

                const randomChoice = ["left", "center", "right"][Math.floor(Math.random() * 3)];

                gameOutput.innerHTML += `<p>You chose ${choice.toUpperCase()} and the opponent chose ${randomChoice.toUpperCase()}</p>`;

                if ((isGoalkeeper && choice === randomChoice) || (!isGoalkeeper && choice !== randomChoice)) {
                    gameOutput.innerHTML += `<p>You ${action}d a shot!!!</p>`;
                    if (isGoalkeeper) {
                        goalieGoals++;
                    } else {
                        kickerGoals++;
                    }
                } else {
                    gameOutput.innerHTML += `<p>Opponent makes the shot ${randomChoice.toUpperCase()}!</p>`;
                    if (isGoalkeeper) {
                        kickerGoals++;
                    } else {
                        goalieGoals++;
                    }
                }

                gameOutput.innerHTML += `<p>Goalie Score: ${goalieGoals} goals</p>`;
                gameOutput.innerHTML += `<p>Kicker Score: ${kickerGoals} goals</p>`;

                if (isGoalkeeper) {
                    goalkeeperTurns++;
                    if (goalkeeperTurns < 5) {
                        setTimeout(() => {
                            penaltyKick(true); // Continue as the goalkeeper
                        }, 1000); // Continue the game after a short delay.
                    } else {
                        gameOutput.innerHTML += "<p>Goalkeeper part is done!</p>";
                        setTimeout(() => {
                            startScorer(); // Start the scorer part
                        }, 1000); // Continue after a short delay.
                    }
                } else {
                    // Check if scorer has taken all 5 shots
                    if (kickerGoals < 5) {
                        setTimeout(() => {
                            penaltyKick(false); // Continue as the scorer
                        }, 1000); // Continue the game after a short delay.
                    } else {
                        gameOutput.innerHTML += "<p>Scorer part is done!</p>";
                        determineWinner(); // Determine the winner
                    }
                }
            }

            function startScorer() {
                gameOutput.innerHTML += "<p>You are now the scorer!</p>";
                goalieGoals = 0;
                kickerGoals = 0;
                goalkeeperTurns = 0;
                penaltyKick(false); // Start as the scorer
            }

            function determineWinner() {
                if (goalieGoals > kickerGoals) {
                    gameOutput.innerHTML += "<p>Goalie wins!</p>";
                } else if (kickerGoals > goalieGoals) {
                    gameOutput.innerHTML += "<p>Kicker wins!</p>";
                } else {
                    gameOutput.innerHTML += "<p>It's a draw!</p>";
                }
            }

            function playGame() {
                gameOutput.innerHTML = "";
                goalieGoals = 0;
                kickerGoals = 0;
                goalkeeperTurns = 0;
                penaltyKick(true); // Start as the goalkeeper
            }

            startButton.addEventListener("click", playGame);
        });
    </script>
</body>
</html>

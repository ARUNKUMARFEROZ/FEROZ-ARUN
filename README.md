# FEROZ-ARUN
ARUN
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>ARUN FEROZ </title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #1a1a1a;
            color: #f1f1f1;
            margin: 0;
            padding: 0;
            text-align: center;
        }

        .container {
            margin-top: 50px;
        }

        .score-board {
            font-size: 2rem;
            margin-bottom: 20px;
        }

        .timer {
            font-size: 1.5rem;
            margin-bottom: 30px;
        }

        .start-btn {
            padding: 10px 20px;
            font-size: 1.2rem;
            background-color: #ff6200;
            border: none;
            color: white;
            cursor: pointer;
            border-radius: 8px;
            transition: background-color 0.3s;
        }

        .start-btn:hover {
            background-color: #e55b00;
        }

        .game-area {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }

        .game-box {
            width: 100px;
            height: 100px;
            margin: 10px;
            background-color: #333;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #fff;
            font-size: 1.5rem;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .game-box:hover {
            background-color: #ff6200;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Welcome to the ARUN GAME WORLD</h1>
        <div class="score-board">
            Score: <span id="score">0</span>
        </div>
        <div class="timer">
            Time Left: <span id="timer">30</span> seconds
        </div>
        <button class="start-btn" onclick="startGame()">Start Game</button>
        
        <div class="game-area" id="gameArea" style="display: none;">
            <!-- Dynamic game boxes will appear here -->
        </div>
    </div>

    <script>
        let score = 0;
        let timeLeft = 30;
        let timerInterval;
        let gameInterval;
        let gameStarted = false;

        // Function to start the game
        function startGame() {
            if (gameStarted) return;
            gameStarted = true;
            document.getElementById('gameArea').style.display = 'flex';
            document.querySelector('.start-btn').disabled = true;

            // Reset the score and time
            score = 0;
            timeLeft = 30;
            document.getElementById('score').textContent = score;
            document.getElementById('timer').textContent = timeLeft;

            // Start the game timer
            timerInterval = setInterval(updateTimer, 1000);
            gameInterval = setInterval(generateGameBox, 1000);
        }

        // Function to update the timer
        function updateTimer() {
            timeLeft--;
            document.getElementById('timer').textContent = timeLeft;

            if (timeLeft <= 0) {
                clearInterval(timerInterval);
                clearInterval(gameInterval);
                endGame();
            }
        }

        // Function to generate random game boxes
        function generateGameBox() {
            const gameArea = document.getElementById('gameArea');
            const gameBox = document.createElement('div');
            gameBox.classList.add('game-box');
            gameBox.textContent = '+1';
            gameBox.style.top = Math.random() * 300 + 'px';
            gameBox.style.left = Math.random() * 400 + 'px';
            
            // Append to the game area
            gameArea.appendChild(gameBox);

            // Add click event to the box
            gameBox.addEventListener('click', function () {
                score++;
                document.getElementById('score').textContent = score;
                gameBox.remove();
            });

            // Remove the box after 1 second
            setTimeout(() => {
                gameBox.remove();
            }, 1000);
        }

        // Function to end the game
        function endGame() {
            gameStarted = false;
            document.querySelector('.start-btn').disabled = false;
            alert('Game Over! Final Score: ' + score);
            document.getElementById('gameArea').style.display = 'none';
        }
    </script>

</body>
</html>

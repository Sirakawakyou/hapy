<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple RPG Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        #game {
            background: #fff;
            border: 2px solid #333;
            width: 80%;
            max-width: 600px;
            padding: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
        #output {
            height: 200px;
            overflow-y: auto;
            border: 1px solid #ccc;
            padding: 10px;
            background: #e9e9e9;
            margin-bottom: 10px;
        }
        #actions button {
            margin: 5px;
            padding: 10px;
            background: #007BFF;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        #actions button:hover {
            background: #0056b3;
        }
    </style>
</head>
<body>
    <div id="game">
        <h1>Simple RPG</h1>
        <div id="output"></div>
        <div id="actions">
            <button onclick="explore()">Explore</button>
            <button onclick="rest()">Rest</button>
            <button onclick="fight()">Fight</button>
        </div>
    </div>

    <script>
        let health = 100;
        let gold = 0;

        function updateOutput(message) {
            const output = document.getElementById('output');
            output.innerHTML += `<p>${message}</p>`;
            output.scrollTop = output.scrollHeight;
        }

        function explore() {
            const events = [
                "You found a treasure chest containing 10 gold!",
                "A wild goblin appeared and attacked you! You lost 20 health.",
                "You found a peaceful meadow and rested for a while. +10 health.",
            ];
            const event = events[Math.floor(Math.random() * events.length)];

            if (event.includes("gold")) {
                gold += 10;
            } else if (event.includes("lost")) {
                health -= 20;
            } else if (event.includes("+10 health")) {
                health = Math.min(100, health + 10);
            }

            updateOutput(event);
            checkGameOver();
        }

        function rest() {
            health = Math.min(100, health + 20);
            updateOutput("You rested and regained 20 health.");
        }

        function fight() {
            const damage = Math.floor(Math.random() * 30) + 10;
            const reward = Math.floor(Math.random() * 15) + 5;

            health -= damage;
            gold += reward;

            updateOutput(`You fought bravely! You took ${damage} damage and earned ${reward} gold.`);
            checkGameOver();
        }

        function checkGameOver() {
            if (health <= 0) {
                updateOutput("Game Over! You have no health left.");
                document.getElementById('actions').style.display = 'none';
            }
        }

        // Initial Message
        updateOutput("Welcome to the Simple RPG! Choose an action to start.");
    </script>
</body>
</html>

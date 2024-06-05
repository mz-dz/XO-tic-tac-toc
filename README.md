# Tic Tac Toe Game

## Description
This project is a simple implementation of the classic Tic Tac Toe game using HTML, CSS, and JavaScript. The game is designed to be visually appealing and user-friendly, allowing two players to take turns marking spaces in a 3×3 grid. The player who succeeds in placing three of their marks in a horizontal, vertical, or diagonal row wins the game.

## Features
- Two-player gameplay
- Interactive UI with smooth transitions and hover effects
- Reset button to restart the game
- Win detection and display of a win message

## Installation
To run this game, simply clone the repository or download the files, and open the `index.html` file in a web browser.

## Usage
1. Open the `index.html` file in a web browser.
2. The game board will be displayed with nine empty cells.
3. Player X starts the game. Click on any empty cell to place your mark.
4. Players take turns clicking on empty cells to place their marks (X or O).
5. The game detects if a player has won and displays a win message.
6. Click the "Reset 🔄" button to start a new game.

## Code Overview
### HTML
The HTML structure includes a container for the game board, buttons for each cell, and a reset button.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Tic Tac Toe</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body class="con">
    <h1>Tic Tac Toe ⭕❌</h1>
    <div class="container">
      <div class="row">
        <button id="r0"></button>
        <button id="r1"></button>
        <button id="r2"></button>
      </div>
      <div class="row">
        <button id="r3"></button>
        <button id="r4"></button>
        <button id="r5"></button>
      </div>
      <div class="row">
        <button id="r6"></button>
        <button id="r7"></button>
        <button id="r8"></button>
      </div>
      <div class="controls">
        <button id="reset">Reset 🔄</button>
      </div>
      <div class="message" id="message"></div>
    </div>
    <script src="script.js"></script>
  </body>
</html>
```

### CSS
The CSS defines the layout and style of the game, including fonts, colors, button styles, and hover effects.

```css
@import url("https://fonts.googleapis.com/css2?family=Amiri+Quran&family=Inter:wght@400;700&display=swap");

:root {
  font-family: "Inter", Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;
  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
  background-color: #242424;
  color: #ffffff;
  padding: 20px;
  box-sizing: border-box;
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #1a1a1a;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  width: 100%;
  filter: drop-shadow(0 0 2em #646cffaa);
}

.row {
  display: flex;
}

.row button {
  height: 100px;
  width: 100px;
  font-size: 24px;
  margin: 5px;
  border: 2px solid #333;
  background-color: #1a1a1a;
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s, filter 0.3s;
  filter: drop-shadow(0 0 1em #646cffaa);
}

.row button:hover {
  background-color: #333;
}

.row button:disabled {
  cursor: not-allowed;
  background-color: #555;
}

.controls {
  margin-top: 20px;
}

#reset {
  padding: 10px 20px;
  font-size: 18px;
  border: none;
  background-color: #007bff;
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s, filter 0.3s;
  filter: drop-shadow(0 0 1em #007bffaa);
}

#reset:hover {
  background-color: #0056b3;
  filter: drop-shadow(0 0 1.5em #0056b3aa);
}

#reset:focus {
  outline: none;
}

.message {
  margin-top: 20px;
  font-size: 24px;
  font-weight: bold;
  color: #fff;
  filter: drop-shadow(0 0 2em #646cffaa);
}
```

### JavaScript
The JavaScript handles the game logic, including player turns, win detection, and resetting the game.

```javascript
let currentPlayer = 'X';
let win = false;
const winningCombinations = [
  [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
  [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
  [0, 4, 8], [2, 4, 6] // diagonals
];

function togglePlayer() {
  currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
}

function checkWin() {
  const buttons = document.querySelectorAll('.row button');
  for (let combination of winningCombinations) {
    const [a, b, c] = combination;
    if (buttons[a].textContent === currentPlayer &&
        buttons[b].textContent === currentPlayer &&
        buttons[c].textContent === currentPlayer) {
      return true;
    }
  }
  return false;
}

function handleClick(event) {
  if (!win && !this.textContent) {
    this.textContent = currentPlayer;
    if (checkWin()) {
      win = true;
      document.getElementById('message').textContent = 'Player ' + currentPlayer + ' wins!🎉';
    } else {
      togglePlayer();
    }
  }
}

function resetGame() {
  const buttons = document.querySelectorAll('.row button');
  buttons.forEach(button => {
    button.textContent = '';
    button.disabled = false;
  });
  currentPlayer = 'X';
  win = false;
  document.getElementById('message').textContent = '';
}

document.querySelectorAll('.row button').forEach(button => {
  button.addEventListener('click', handleClick);
});

document.getElementById('reset').addEventListener('click', resetGame);
```

## Contributing
Contributions are welcome! Please feel free to submit a Pull Request or open an issue for any bugs or feature requests.

## License
This project is licensed under the MIT License.

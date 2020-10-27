# Tic-Tac-Toe

## A simple tic-tac-toe game in vanilla javascript. 👁️👅👁️

Modes:
* PvP
* PvAI

## How to play
1. Go to [repo](https://github.com/ruvvet/tic-tac-toe) on Github profile.
2. `fork` + `clone`.
3. Clone to local.
```text
git clone https://github.com/ruvvet/tic-tac-toe.git
```
4. Find `tic-tac-toe` directory.
5. Open `index.html` in browser.
```text
open index.html
```
6. Done.

## Rules
Basic Tic-Tac-Toe. Get 3 in a row. Go. 🎰

### PvP
![Imgur](https://i.imgur.com/urhn4bg.gif)

### PvAi
![Imgur](https://i.imgur.com/0MSWJNq.gif)

# Code snippets
### How information is parsed and passed from the board to the page.
Creating the board in HTML. Initializing players and internal game-state board in JS.

```javascript
// JS
// nested array board keeps state of the game
const board = [...Array(3)].map(() => Array(3).fill(null));
//board looks like this:
// [[null, null, null],
//[null, null, null],
//[null, null, null]]

//creating our players
let players = [
    {player: 1, mark: 'X', img: "img/cross.png", score: 0},
    {player: 2, mark: 'O', img: "img/heart.png", score: 0}
];
```
```html
<!-- HTML -->
<!-- each button's ID is designated by it's location in the board -->
<!-- this allows us to get the id of the clicked button -->
<!-- and parse the ID to update the array to update the game state -->
<div class="board">
<!-- Row 1 -->
<button class="space" id="00"></button>
<button class="space" id="01"></button>
<button class="space" id="02"></button>
<!-- Row 2 -->
<button class="space" id="10"></button>
<button class="space" id="11"></button>
<button class="space" id="12"></button>
<!-- Row 3 -->
<button class="space" id="20"></button>
<button class="space" id="21"></button>
<button class="space" id="22"></button>
</div>
```
### How we activate actions from the page to the internal code
All buttons share the same class, which we take advantage of with a loop to execute the update function.

```javascript
// all buttons have the space class
// spaces is an array of all those buttons
let spaces = document.querySelectorAll('.space');
// initializes each div space with a clear space
// each div space is clickable
// when clicked, calls the update space function which update the inner array
for (let i = 0; i < spaces.length; i++) {
    spaces[i].innerHTML = '';
    // we call the update space function + pass the element that was clicked
    spaces[i].onclick = () => updateSpace(spaces[i]);
}
```
By calling .id on the element passed into the function, we get the element ID which can then be parsed into x- and y- coordinates to locate it in the internal game board array.

```javascript
// after clicking a space, the udpate space function is called
const updateSpace = (space) => {
    // we get the id of the div space in order to update the board array
    //
    let location = space.id.split('').map(x => parseInt(x));
    let x = location[0];
    let y = location[1];
    //...
```
### How we control game flow + logic.
Check if board space is null (then the move is valid) >> If valid, print to the page and update the game-state array.

```javascript
// if board space in array is empty, the move is valid
if (!board[x][y]) {

    // if the player is x, print x
    let playerIndex = players.indexOf(currentPlayer);
    space.innerHTML = `<img src="${players[playerIndex].img}">`;

    // call update board function with locations
    board[x][y] = currentPlayer['player'];

```
### How we control game flow.
Toggling the player back and forth between moves.

```javascript
// ternary operator to toggle players
// if current player is player[0], then set current player to player[1], else [0]
    currentPlayer = (currentPlayer == players[0] ? players[1] : players[0]);

```
### How we find a winner.
Checking for a winner.
```javascript
// loop through each element in combos (rows + col + diagonals)
for (let i = 0; i < combos.length; i++){
    // If every element is the same, and not null - there is a winner
    if (combos[i][0] !== null && new Set(combos[i]).size == 1) {
        currentPlayer['score'] ++;
        return true;
    }
}
// If no winner was found, check if the board is full, that would be a tie:
for(let i = 0; i < board.length; i++) {
    if (board[i].includes(null)) {
        return false;
    }
}
return 'Tie';
```

Some CSS (I didn't use the glow effect because it didn't look clean).
```css
.player {
  grid-area: left;
  /* background-color: #ffffff90; */
  font-size: 30px;
  color: rgb(0, 0, 0);
  text-align: center;
  padding: 80% 0 0 0;
  /* -webkit-animation: glow 3s ease-in-out infinite alternate;
  -moz-animation: glow 3s ease-in-out infinite alternate;
  animation: glow 3s ease-in-out infinite alternate; */
}

@-webkit-keyframes glow{
  from {
    text-shadow: 0 0 10px #fff,
    0 0 20px #fff, 0 0 30px #e60073,
    0 0 40px #e60073, 0 0 50px #e60073,
    0 0 60px #e60073, 0 0 70px #e60073;
  }
  to {
    text-shadow: 0 0 20px #fff,
    0 0 30px #ff4da6, 0 0 40px #ff4da6,
    0 0 50px #ff4da6, 0 0 60px #ff4da6,
    0 0 70px #ff4da6, 0 0 80px #ff4da6;
  }
}
```

### Future To-Do List

- [ ] Add hard-mode PvAI w/ max-min algorithm
- [ ] Highlight winning lines


| Functions           | Description |
| -----------         | ----------- |
| `printStuff()`      | Pretty printing of the start/reset/next/pvp/pvai buttons|
| `pvp()`      | Starts a PvP game|
| `pvai()`      | starts a PvAi game|
| `toggleTurn()`      | Just controls the side divs when it's each players turn to move|
| `checkWinner()`      | Checks for a winner|
| `aiMove()`      | Controls random generator for AI to select a spot|
| `resetGame()`      | Resets the board state and player score.|

| -Some- Variables       | Description |
| -----------         | ----------- |
| `players`      | Player objects in an array|
| `board`      | Nested array which maintains game-state|
| `spaces`      | Array of all buttons on the board|
| `currentPlayer`      |Current Player which is toggled back + forth|
| `combos`      | An array of all possible winning arrays (rows + col + diagonals)|

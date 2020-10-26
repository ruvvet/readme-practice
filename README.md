# Tic-Tac-Toe

## A simple tic-tac-toe game in vanilla javascript. 👁️👅👁️

* Contains PvP and PvAi modes.
* Still needs to be optimized.

## How to Play
3 in a row wins. 🎰

### PvP
![Imgur](https://i.imgur.com/urhn4bg.gifv)

### PvAi
![Imgur](https://i.imgur.com/0MSWJNq.gifv)

### To-Do

- [ ] Add hard-mode PvAI w/ max-min algorithm
- [ ] Highlight winning lines


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


```javascript
// Some of the code for fun
// nested array board keeps state of the game
const board = [...Array(3)].map(() => Array(3).fill(null));
//...
// checking for a winner means looping through all rows/col/diagonals
// checks if null, if its a 1 or a 2, etc. to determine game outcome
for (let i = 0; i < combos.length; i++){
    if (combos[i][0] !== null && new Set(combos[i]).size == 1) {
        currentPlayer['score'] +=1
        return true;
    }
}
// look inside app.js for more
```

| Functions           | Description |
| -----------         | ----------- |
| functions go here      | description goes here |



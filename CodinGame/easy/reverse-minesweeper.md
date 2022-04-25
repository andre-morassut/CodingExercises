# Reverse Minesweeper

## Description

Level : easy

### Goal

Given a grid of mine locations (where `.` are empty cells and `x` are mines), your goal is to display the grid like it appears if you win the game.

Each position is a digit indicating the number of mines bordering it (including diagonals). The mines (`x`) don't appear anymore. Mines and positions that do not border any mines both appear as empty cells (`.`).

**Input**
```
Line 1 : an integer w for the width of the grid.
Line 2 : an integer h for the height of the grid.
Next h lines : each line of the minefield, with dots (.) or mines (x).
```

**Output**
```
h lines of width w showing the completed game of Minesweeper.
```

**Constraints**
```
1 <= w <= 30
1 <= h <= 30
```

**Example**

**Input**
```
16
9
................
................
................
................
................
....x...........
................
................
................
```

**Output**
```
................
................
................
................
...111..........
...1.1..........
...111..........
................
................
```

## Code

```js
const w = parseInt(readline());
const h = parseInt(readline());

const m = Array(h)
        .fill()
        .map(v => [...readline()])
        .reduce((acc, cur, i, arr) => boom(i, arr), [])
        .map(v => v.join(''))
        .join('\n')
        .replaceAll('x', '.');
console.log(m);

function boom(y, arr) {
    let yMinOk = y > 0;
    let yMaxOk = y < h - 1;
    [...arr[y].join('').matchAll(/x/g)].map(v => v.index).forEach(x => {
        let xMinOk = x > 0;
        let xMaxOk = x < w - 1; 
        if (yMinOk && xMinOk) arr[y-1][x-1] = inc(arr[y-1][x-1]); // UL
        if (yMinOk) arr[y-1][x] = inc(arr[y-1][x]); // U
        if (yMinOk && xMaxOk) arr[y-1][x+1] = inc(arr[y-1][x+1]); // UR
        if (xMinOk) arr[y][x-1] = inc(arr[y][x-1]); // L
        if (xMaxOk) arr[y][x+1] = inc(arr[y][x+1]); // R
        if (yMaxOk && xMinOk) arr[y+1][x-1] = inc(arr[y+1][x-1]); // DL
        if (yMaxOk) arr[y+1][x] = inc(arr[y+1][x]); // D
        if (yMaxOk && xMaxOk) arr[y+1][x+1] = inc(arr[y+1][x+1]); // DR
    });
    return arr;
}

function inc(cell) {
    if (cell === 'x') return 'x';
    if (cell === '.') return 1; 
    return +cell + 1;
}
```

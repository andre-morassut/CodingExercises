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

## Another answer (really cool, by luigi_gelato)

luigi_gelato codinGame profile URL : https://www.codingame.com/profile/e6fd6e26f416690cbe40734e5165e8fc8515132

```js
const w = +readline();
const h = +readline();
const grid = [...Array(h)].map(_ => readline().split(''));
const neighbors = [[-1,-1],[0,-1],[1,-1],[-1,0],[1,0],[-1,1],[0,1],[1,1]];

for (let y = 0; y < h; y++) {
    for (let x = 0; x < w; x++) {
        if (grid[y][x] == 'x') {
            neighbors
                .map(([dx,dy]) => [x+dx,y+dy])
                .filter(([x,y]) => x >= 0 && x < w && y >= 0 && y < h)
                .filter(([x,y]) => grid[y][x] != 'x')
                .forEach(([x,y]) => grid[y][x] = +grid[y][x] + 1 || 1);
        }
    }
}

grid.forEach(row => console.log(row.join('').replace(/x/g, '.')));
```

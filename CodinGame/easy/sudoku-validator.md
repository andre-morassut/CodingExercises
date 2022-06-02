# Sudoku Validator

## Description

Level : easy

### Goal

You get a sudoku grid from a player and you have to check if it has been correctly filled.

A sudoku grid consists of 9×9 = 81 cells split in 9 sub-grids of 3×3 = 9 cells.

For the grid to be correct, each row must contain one occurrence of each digit (1 to 9), each column must contain one occurrence of each digit (1 to 9) and each sub-grid must contain one occurrence of each digit (1 to 9).

You shall answer true if the grid is correct or false if it is not.

**Input**
```
9 rows of 9 space-separated digits representing the sudoku grid.
```

**Output**
```
true or false
```

**Constraints**
```
For each digit n in the grid: 1 ≤ n ≤ 9.
```

**Example**

**Input**
```
1 2 3 4 5 6 7 8 9
4 5 6 7 8 9 1 2 3
7 8 9 1 2 3 4 5 6
9 1 2 3 4 5 6 7 8
3 4 5 6 7 8 9 1 2
6 7 8 9 1 2 3 4 5
8 9 1 2 3 4 5 6 7
2 3 4 5 6 7 8 9 1
5 6 7 8 9 1 2 3 4
```

**Output**
```
true
```

## Code

```js
let validate = nums => nums.sort((a, b) => a - b).join('') === '123456789';
let grid = Array(9).fill().map(v => readline().split(' ').map(w => +w));
let pivo = Array(9).fill().map((_, i) => Array(9).fill().map((_, j) => grid[j][i]));
let subs = Array(9).fill();
subs.forEach((_, i, arr) => {
    grid[i].forEach((w, j) => {
        let index = (3 * Math.floor(i / 3)) + Math.floor(j / 3);
        if (!arr[index]) arr[index] = [];
        arr[index].push(w);
    })
});

// validate rows
let rowsOk = grid.reduce((acc, cur) => acc && validate(cur), true);
// validate columns
let colsOk = pivo.reduce((acc, cur) => acc && validate(cur), true);
// validate sub grids
let subsOk = subs.reduce((acc, cur) => acc && validate(cur), true);;

console.log(rowsOk && colsOk && subsOk);
```

And check out this answer by Djoums (CodinGame profile: https://www.codingame.com/profile/f0b5a892e52b5ec167931b7bdf52eb982136521), really neat usage of `every` and `includes`.

```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const grid = [...new Array(9)].map(_ => readline().split(' ').map(i => +i));
console.log(
    grid.every(row => numbers.every(n => row.includes(n))) &&
    grid.map((_, i) => grid.map(row => row[i]))
        .every(col => numbers.every(n => col.includes(n))) &&
    grid.map((_, i) => grid.map((_, j) => grid[3 * Math.floor(i / 3) + Math.floor(j / 3)][3 * (i % 3) + j % 3]))
        .every(square => numbers.every(n => square.includes(n))));
```

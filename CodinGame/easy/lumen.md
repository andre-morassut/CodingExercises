# Lumen

## Description

Level : easy 

### Goal

THEY put you in a square shape room, with N meters on each side.

THEY want to know everything about you.

THEY are observing you.

THEY placed some candles in the room.

Every candle makes L "light" in the spot they are, and every spot in square shape gets one less "light" as the next ones. If a spot is touched by two candles, it will have the larger "light" it can have. Every spot has the base light of 0.

You can hide only, if you find a dark spot which has 0 "light".
How many dark spots you have?

You will receive a map of the room, with the empty places (X) and Candles (C) in N rows, each character separated by a space.

**Example for the light spread N = 5, L = 3:**
```
X X X X X
X C X X X
X X X X X
X X X X X
X X X X X

2 2 2 1 0
2 3 2 1 0
2 2 2 1 0
1 1 1 1 0
0 0 0 0 0
```

**Input**
```
Line 1: An integer N for the length of one side of the room.
Line 2: An integer L for the base light of the candles.
Next N lines: N number of characters (as c), separated by one space.
```

**Output**
```
Line 1 : The number of places with zero light.
```

**Constraints**
```
0 < N <= 25
0 < L < 10
```

**Example**

**Input**
```
5
3
X X X X X
X C X X X
X X X X X
X X X X X
X X X X X
```

**Output**
```
9
```

## Code

### Solution \#1 - Count lighted cells to decrement dark cell count

```js
const N = parseInt(readline());
const L = parseInt(readline());
let noLight = N * N;
let m = Array(N).fill().map(v => [...(readline().replaceAll(' ', ''))]);
for (let x = 0; x < N; x++) 
    for (let y = 0; y < N; y++) 
        if (m[y][x] == 'C') noLight -= light(x, y, m);

console.log(noLight);

function light(x, y, arr) {
    arr[y][x] = '';
    let noLight = 1;
    for (let xI = Math.max(x - L + 1, 0); xI <= Math.min(x + L - 1, N - 1); xI++) {
        for (let yI = Math.max(y - L + 1, 0); yI <= Math.min(y + L - 1, N - 1); yI++) {
            if (arr[yI][xI] == 'X') {
                arr[yI][xI] = '';
                noLight++;
            }
        }
    }
    return noLight;
}  
```

### Solution \#2 - Render illumination and count dark cells

```js
const N = parseInt(readline());
const L = parseInt(readline());
let result = Array(N).fill().map(v => [...(readline().replaceAll('X', '0'))].filter(v => v !== ' ')).reduce((_, __, y, arr) => {
    let x = arr[y].indexOf('C');
    while(x > -1) {
        x = impact(x, y, arr);
    }
    return arr;
}, []).reduce((prev, cur, y, arr) => prev += +cur.reduce((p, c) => p += c == '0' ? 1 : 0, 0), 0); 

console.log(result);

function impact(x, y, arr) {
    arr[y][x] = L;
    for (let xI = Math.max(x - L + 1, 0); xI <= Math.min(x + L - 1, N - 1); xI++) {
        for (let yI = Math.max(y - L + 1, 0); yI <= Math.min(y + L - 1, N - 1); yI++) {
            arr[yI][xI] = arr[yI][xI] != 'C' ? Math.max(arr[yI][xI], L - Math.max(yI - y, xI- x)) : 'C';
        }
    }
    return arr[y].indexOf('C', x);
}
```

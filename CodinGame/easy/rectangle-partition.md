# Title

This is the title.

## Description

Level : easy

### Goal

There is a rectangle of given width w and height h,

On the width side, you are given a list of measurements.
On the height side, you are given another list of measurements.

Draw perpendicular lines from the measurements to partition the rectangle into smaller rectangles.

In all sub-rectangles (include the combinations of smaller rectangles), how many of them are squares?


**Example**
```
w = 10
h = 5
measurements on x-axis: 2, 5
measurements on y-axis: 3

   ___2______5__________ 
  |   |      |          |
  |   |      |          |
 3|___|______|__________|
  |   |      |          |
  |___|______|__________|
```
Number of squares in sub-rectangles = 4 (one 2x2, one 3x3, two 5x5)

**Input**
```
Line 1: Integers w h countX countY, separated by space
Line 2: list of measurements on the width side, countX integers separated by space, sorted in asc order
Line 3: list of measurements on the height side, countY integers separated by space, sorted in asc order
```

**Output**
```
Line 1: the number of squares in sub-rectangles created by the added lines
```

**Constraints**
```
1 ≤ w, h ≤ 20,000
1 ≤ number of measurements on each axis ≤ 500
```

**Example**

**Input**
```
10 5 2 1
2 5
3
```

**Output**
```
4
```

## Code

```js
let xArray = [0];
let yArray = [0];
/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/
var inputs = readline().split(' ');
const w = parseInt(inputs[0]);
const h = parseInt(inputs[1]);
const countX = parseInt(inputs[2]);
const countY = parseInt(inputs[3]);
var inputs = readline().split(' ');
for (let i = 0; i < countX; i++) {
    xArray.push(parseInt(inputs[i]));
}
var inputs = readline().split(' ');
for (let i = 0; i < countY; i++) {
    yArray.push(parseInt(inputs[i]));
}

// Write an answer using console.log()
// To debug: console.error('Debug messages...');
// https://www.codingame.com/ide/puzzle/rectangle-partition
xArray.push(w);
yArray.push(h);
let answer = 0;
// transform to array of possible distances on both axis
let xDistances = Array.from(xArray).splice(1, xArray.length - 1);
let yDistances = Array.from(yArray).splice(1, yArray.length - 1);
for (let i = 1; i < xArray.length; i++) {
    for (let j = i + 1; j < xArray.length; j++) {
        xDistances.push(xArray[j] - xArray[i]);
    }
}
for (let i = 1; i < yArray.length; i++) {
    for (let j = i + 1; j < yArray.length; j++) {
        yDistances.push(yArray[j] - yArray[i]);
    }
}
// each match means a square is found
for (let i = 0; i < xDistances.length; i++) {
    let start = yDistances.indexOf(xDistances[i]);
    while (start > -1) {
        start = yDistances.indexOf(xDistances[i], start + 1);
        answer++;
    }
}
console.log(answer);


// FTR 1 : Clever solution
// note the pattern : using a sliced copy of x positions to compute distances
/*
const [W, H, _, __] = readline().split(' ').map(n => +n);
const MW = [0].concat(readline().split(' ').map(n => +n)).concat([W]);
const MH = [0].concat(readline().split(' ').map(n => +n)).concat([H]);
let µ = a => console.error(a);
µ(`MW:${MW}`);
µ(`MH:${MH}`);
var squares = 0;
for (let y = 0; y < MH.length - 1; y++) {
    for (let x = 0; x < MW.length - 1; x++) {
        let sliced = MW.slice(x + 1, MW.length);
        µ(`y:${y},x:${x} : sliced:${sliced}`);
        squares += sliced.filter(next => {
            µ(`MH.includes(MH[y]:${MH[y]} + next:${next} - MW[x:${x}]:${MW[x]}) = MH.includes(${MH[y] + next - MW[x]}) = ${MH.includes(MH[y] + next - MW[x])}`);
            return MH.includes(MH[y] + next - MW[x])
        }).length;

        //squares += MW.slice(x + 1, MW.length).filter(next => MH.includes(MH[y] + next - MW[x])).length;
    }
}
console.log(squares);
*/

// FTR 2 : Example of a "naive" solution => not optimized enough (all cases are evaluated)
/*
for (let x1 = 0; x1 < xArray.length; x1++) {
    for (let x2 = (x1 + 1); x2 < xArray.length; x2++) {
        for (let y1 = 0; y1 < yArray.length; y1++) {
            for (let y2 = (y1 + 1); y2 < yArray.length; y2++) {
                µ(`${xArray[x1]}, ${yArray[y1]} | ${xArray[x2]}, ${yArray[y2]}`);
                if ((xArray[x2] - xArray[x1]) === (yArray[y2] - yArray[y1])) {
                    answer++;
                }
            }
        }
    }    
}
console.log(answer);
*/

```

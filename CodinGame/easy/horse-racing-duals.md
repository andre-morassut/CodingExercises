# Horse-racing Duals

## Description

Level : easy

### Goal
Casablanca’s hippodrome is organizing a new type of horse racing: duals. During a dual, only two horses will participate in the race. In order for the race to be interesting, it is necessary to try to select two horses with similar strength.

Write a program which, using a given number of strengths, identifies the two closest strengths and shows their difference with an integer (≥ 0).

**Input**
```
Line 1: Number N of horses
The N following lines: the strength Pi of each horse. Pi is an integer.
```
**Output**
```
The difference D between the two closest strengths. D is an integer greater than or equal to 0.
```
**Constraints**
```
1 < N  < 100000
0 < Pi ≤ 10000000
```
#### Example
**Input**
```
3
5
8
9
```
**Output**
```
1
```

## Code

```js
function calcPowerDelta(horseA, horseB) {
    return Math.abs(horseA - horseB);
}
/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/
const N = parseInt(readline());

// push all horses in an array and sort it
let horses = [];
let minPowerDelta = Number.MAX_SAFE_INTEGER;
for (let i = 0; i < N; i++) {
    horses.push(parseInt(readline()));
}
horses.sort((a, b) => b - a);
// compute each delta keeping the minimum in memory
for (let i = 1; i < horses.length; i++) {
    let curPowerDelta = calcPowerDelta(horses[i - 1], horses[i]);
    minPowerDelta = curPowerDelta < minPowerDelta ? curPowerDelta : minPowerDelta;
}

// Write an answer using console.log()
// To debug: console.error('Debug messages...');

console.log(minPowerDelta);
```


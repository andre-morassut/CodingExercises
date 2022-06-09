# Mountain Map

## Description

Level : easy

### Goal

The task here is to print the ASCII representation of `n` mountains where the height of each mountain is given.

**Input**
```
Line 1: an integer n for the number of mountains
Line 2: n space-separated integers for the height of each mountain
```
**Output**
```
An ASCII representation of the mountain where each rise in the mountain is represented by '/' and fall by '\'
(Output lines shall not contain trailing spaces)
```
**Constraints**
```
0<n<15
0<height<15
(every mountain's base starts on the bottom-most line)
```
**Example**

**Input**
```
3
1 2 1
```
**Output**
```
   /\
/\/  \/\
```

## Code

```js
readline(); // the number of mountains is not used
const inputs = readline().split(' ').map(v => +v);

// function drawing a single mountain
let draw = h => Array(h).fill().map((_, i) => {
    let row = Array(h * 2).fill(' ');
    row[h - 1 - i] = '/';
    row[h + i] = '\\';
    return [row.join('')];
});

// draw each mountain and cumulate it in mountains array
let high = Math.max(...inputs);
let mountains = Array(high).fill([]);
inputs.forEach((_, i) => {
    let curMountain = draw(inputs[i]);
    mountains = mountains.map((v, j) => {
        if (j >= high - curMountain.length) {
            return v.concat(curMountain[j - (high - curMountain.length)]);
        } else {
            return v.concat(Array(inputs[i] * 2).fill(' '));
        }
    });
});

console.log(mountains.map(v => v.join('').trimEnd()).join('\n'));
```


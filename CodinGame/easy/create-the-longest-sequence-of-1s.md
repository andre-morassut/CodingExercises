# Create the longest sequence of 1s

## Description

Level : easy

### Goal

Given some bitstring b, you may change one bit from a 0 to a 1 in order to create the longest possible sequence of consecutive 1s. Output the length of the resulting longest sequence.

Example: `11011101111`

Flipping the second `0` results in `11011111111`, where the longest sequence of 1s is `8` long.

**Input**
```
Line 1: The bitstring b
```

**Output**
```
Line 1: The length of the longest possible sequence of 1s after flipping one bit
```

**Constraints**
```
0 < number of bits in b < 1000
b contains at least one 0
```

**Example**

**Input**
```
00
```

**Output**
```
1
```

## Code

```js
const b = readline();
let matches = [...b.matchAll(/0*(1*)0*/gm)];
// convert to ['sequence of 1', indexStart, indexEnd]
let sequences = matches.reduce((a, v) => v[0] !== '' ? a.concat([[v[1], b.indexOf(v[1], v.index)]]) : a, [])
                       .map(v => v.concat(v[1] + v[0].length));
// compare joinable sequences and individual sequences
let longuest = sequences.reduce((a, v, i, arr) => {
    if ((i < arr.length - 1) && (v[2] === arr[i + 1][1] - 1)) {
        a = Math.max(a, v[0].length + arr[i + 1][0].length + 1);
    }
    a = Math.max(a, v[0].length + 1);
    return a;
}, 1);

console.log(longuest);
```

I took a long path with this one, it can be simplified to :

```js
console.log(readline().split("0")
             .map(x => x.length)
             .reduce((a, v, i, m) =>
                Math.max(a, v + (m[i+1]||0) + 1)
                , 0));
```

# Offset Arrays

## Description

Level : easy

### Goal

To settle the debate of 0-based vs 1-based indexing I have created a language where you must explicitly state the range of indices an array should have.

For example, given an array definition "A[-1..1] = 1 2 3", you would have:
* A[-1] = 1
* A[0] = 2
* A[1] = 3

You are given a list of n array definitions and your job is to figure out what number is found in a given index i of an array arr. Note that the indexing operations may be nested (in the above example, A[A[-1]] would produce result 3).

**Input**
```
Line 1: An integer n for the number of array assignments
Next n lines: One array assignment per line: array_identifier [ first_index .. last_index ] = last_index - first_index + 1 integers separated by space
Line n+2: Element to print: arr [ i ]
```
**Output**
```
A single integer
```

**Constraints**
```
1 <= n <= 100
Each array name consists of only uppercase letters (A to Z)
Array lengths are between 1 and 100 (no empty arrays)
Indexing operations have at most 50 levels of nesting
Indices are always within bounds in the test cases
```

**Example**

**Input**
```
3
A[-1..1] = 1 2 3
B[3..7] = 3 4 5 6 7
C[-2..1] = 1 2 3 4
A[0]
```

**Output**
```
2
```

## Code

```js
const n = +readline();
const format = /^([A-Z]+)[\[]{1}([-]?\d+)[\.]{2}([-]?\d+)[\]][\s][=](([\s][-]?[\d]+)+)$/;
let data = Array(n).fill().reduce((prev, cur) => {
    let parts = format.exec(readline());
    let numbers = parts[4].trim().split(' ');
    let index = 0;
    prev[parts[1]] = {};
    for (let i = +parts[2]; i < +parts[3] + 1; i++) {
        prev[parts[1]][i] = numbers[index];
        index++;
    }
    return prev;
}, {});
const x = readline();

let firstIndex = x.substring(x.lastIndexOf('[') + 1, x.indexOf(']'));
let result = x.substring(0, x.lastIndexOf('[')).split('[')
    .reduceRight((prev, cur) => data[cur][prev], firstIndex);

console.log(result);
```

Also, you can check out this concise program by Djoums (CodinGame profile : https://www.codingame.com/profile/f0b5a892e52b5ec167931b7bdf52eb982136521) : 

```js
const evaluateValue = (value, arr, str) => arr.values[evaluate(str.slice(value.length + 1, -1)) - arr.offset];
const parseValue = (value, str) => !isNaN(value) ? +value : evaluateValue(value, arrays.get(value), str);
const evaluate = (str) => parseValue(str.match(/[^\[]+/)[0], str);

const arrays = new Map([...Array(+readline())]
    .map(readline)
    .map(s => [s.match(/^[^\[]+/)[0], { offset: +s.match(/(?<=\[)[^\.]+/)[0], values: s.match(/(?<= )[^\= ]+/g).map(Number) }]));
console.log(evaluate(readline()));
```

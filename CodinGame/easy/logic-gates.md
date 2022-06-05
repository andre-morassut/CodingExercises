# Logic gates

## Description

Level : easy

### Goal

A logic gate is an electronic device implementing a boolean function, performing a logical operation on one or more binary inputs and producing a single binary output.

Given `n` input signal names and their respective data, and `m` output signal names with their respective type of gate and two input signal names, provide `m` output signal names and their respective data, in the same order as provided in input description.

All type of gates will always have two inputs and one output.

All input signal data always have the same length.

The type of gates are :
* AND : performs a logical AND operation.
* OR : performs a logical OR operation.
* XOR : performs a logical exclusive OR operation.
* NAND : performs a logical inverted AND operation.
* NOR : performs a logical inverted OR operation.
* NXOR : performs a logical inverted exclusive OR operation.

Signals are represented with underscore and minus characters, an undescore matching a low level (0, or false) and a minus matching a high level (1, or true).

**Input**
```
Line 1 : n number of input signals.
Line 2 : m number of output signals.
n next lines : two space separated strings : name of input signal, then signal form.
m next lines : four space separated strings : name of output signal, then type of logic gate, then first input name, then second input name.
```
**Output**
```
m lines : two space separated strings : name of output signal, then signal form.
Constraints
1 ≤ n ≤ 4
1 ≤ m ≤ 16
```
**Example**

**Input**
```
2
3
A __---___---___---___---___
B ____---___---___---___---_
C AND A B
D OR A B
E XOR A B
```
**Output**
```
C ____-_____-_____-_____-___
D __-----_-----_-----_-----_
E __--_--_--_--_--_--_--_--_
```

## Code

```js
const OP = ['AND', 'NAND', 'NOR', 'NXOR', 'OR', 'XOR'];
const FC = [
    (x, y) => x && y, 
    (x, y) => !(x && y), 
    (x, y) => !(x || y), 
    (x, y) => !(x != y), 
    (x, y) => x || y, 
    (x, y) => x != y
];

const n = +readline();
const m = +readline();

let input = Array(n).fill().map(v => readline().split(' ').map((w, j) => j === 1 ? w.replaceAll(/_/g, 0).replaceAll(/-/g, 1).split('') : w).flat());
let specs = Array(m).fill().map(v => readline().split(/\s/g));
let result = specs.reduce((acc, cur, i, prev) => {
    let res = [cur[0], ' '];
    let in1 = input.filter(v => v[0] === cur[2]).flat();
    let in2 = input.filter(v => v[0] === cur[3]).flat();
    let out = Array(Math.max(0, in1.length - 1)).fill().map((_, i) => FC[OP.indexOf(cur[1])](!!+in1[i + 1], !!+in2[i + 1]));
    return acc.concat([res.concat(out.join('').replaceAll(false,'_').replaceAll(true, '-'))]);
}, []);

console.log(result.map(v => v.join('')).join('\n'));
```


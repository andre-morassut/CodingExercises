# Are The Clumps Normal

## Description

Level : easy

### Goal

For a given multi-digit number N, determine on what single-digit positive number B it first deviates from the normal behavior of congruent clumping, if any.

What does that mean? Consider as an example:
```
N = 157285
B = 2
```

Split up the digits of N into a minimum number of clumps such that all of the digits D in each clump are modularly congruent in base B (meaning D % B is the same value):

```
clumps = [157, 28, 5]
D % B  = [1,   0,  1]
```

Notice how for base 2, there are 3 clumps in this example. It can be observed that there would be more clumps if we used base 3 instead:

```
clumps = [1, 5, 7, 285]
D % B  = [1, 2, 1, 2]
```

In fact, for the number 157285, the number of clumps for each base from 1-9 is nondecreasing.

```
N = 157285
base 1: [157285]
base 2: [157, 28, 5]
base 3: [1, 5, 7, 285]
base 4: [15, 7, 2, 8, 5]
base 5: [1, 5, 72, 8, 5]
base 6: [1, 5, 7, 28, 5]
base 7: [1, 5, 7, 2, 8, 5]
base 8: [1, 5, 7, 2, 8, 5]
base 9: [1, 5, 7, 2, 8, 5]
```

We will call this property the normal behavior of congruent clumping. However, not all numbers do this. For example, the number 25747 has 4 clumps in base 2 but only 2 clumps in base 3:

```
N = 25747
base 2: [2, 57, 4, 7]
base 3: [25, 747]
```

For this N, since base 3 contains less clumps than base 2, we would say the number deviates from the normal behavior of congruent clumping at base 3.

Some numbers only deviate on the higher values of B. For example, the number 338066 is normal up until base 8:

```
N = 338066
base 7: [33, 8, 0, 66]
base 8: [33, 80, 66]
```

**Input**
```
Line 1: N given as a string
```
**Output**
```
Either a digit B, from 1 to 9 inclusively, indicating the first deviation from the normal behavior of congruent clumping, or Normal if there is no deviation
```

**Constraints**
```
10 ≤ N ≤ 10^1000
```

**Example**

**Input**
```
157285
```

**Output**
```
Normal
```

## Code

The approach is to count the number of clumps for each base and track a decrease of this number when the base is incremented.

Functional.

```js
const N = readline();
let check = Array(9).fill() 
        // fill with the number of clumps for each base 
        .map((v, b) => [...N].reduce((prev, cur, i, arr) => (cur % (b + 1) === arr[i - 1] % (b + 1)) ? prev : prev + 1, 0))
        // reduce to 0 if normal or to the index of the deviation (decrease in the number of clumps)
        .reduce((prev, cur, i, arr) => (cur < arr[i - 1] && prev === 0) ? i + 1 : prev, 0);
console.log(check === 0 ? 'Normal' : check);
```

Procedural.

```js
const N = [...readline()];
let check = 0;
let clumps = [];
mainLoop: for (let i = 0; i < 9; i++) {
    let numberOfClumps = 0;
    // compute clump count for each base
    for (let j = 0; j < N.length; j++) {
        if (N[j] % (i + 1) !== N[j - 1] % (i + 1)) {
            numberOfClumps++;
        }
    }
    clumps.push(numberOfClumps);
    // check for decrease pattern 
    if (clumps[i] < clumps[i - 1]) {
        check = i + 1;
        break mainLoop; // break early if found
    }
}
console.log(check === 0 ? 'Normal' : check);
```

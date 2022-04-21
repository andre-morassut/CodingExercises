# Temperatures

## Description

Level : easy

### Goal
In this exercise, you have to analyze records of temperature to find the closest to zero.


	
Sample temperatures
Here, -1 is the closest to 0.
 	Rules
Write a program that prints the temperature closest to 0 among input data. If two numbers are equally close to zero, positive integer has to be considered closest to zero (for instance, if the temperatures are -5 and 5, then display 5).
 	Game Input
Your program must read the data from the standard input and write the result on the standard output.
Input
Line 1: N, the number of temperatures to analyze

Line 2: A string with the N temperatures expressed as integers ranging from -273 to 5526

Output
Display 0 (zero) if no temperatures are provided. Otherwise, display the temperature closest to 0.
Constraints
0 ≤ N < 10000
Example
Input
5
1 -2 -8 4 5
Output
1

## Code

```js
/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/

const n = parseInt(readline()); // the number of temperatures to analyse
var inputs = readline().split(' ');

let zeroClosestResult = 0; // the result, initialized to the default value if no inputs

if (inputs.length > 0) {
    let deltaArray = inputs.map(input => input ? parseInt(input) : Infinity); // parse array replacing non ints value by infinity (code is therefore immune to arrays like [1, 5, -2, NaN])
    // separate negative and positive values in different arrays
    let positiveTemps = inputs.filter(input => parseInt(input) > 0);
    let negativeTemps = inputs.filter(input => parseInt(input) < 0);
    // compute lowest deltas
    let positiveRes = Math.min(...positiveTemps);
    let negativeRes = Math.max(...negativeTemps);
    // return closest
    if (Math.abs(positiveRes) != Infinity || Math.abs(negativeRes) != Infinity) {
        if (positiveRes <= Math.abs(negativeRes)) {
            zeroClosestResult = positiveRes;
        } else {
            zeroClosestResult = negativeRes;
        } 
    }
}



// Write an answer using console.log()
// To debug: console.error('Debug messages...');

console.log(zeroClosestResult);
```


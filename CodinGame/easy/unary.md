# Unary

## Description

Level : easy

### Goal
Binary with 0 and 1 is good, but binary with only 0, or almost, is even better!

Write a program that takes an incoming message as input and displays as output the message encoded using this method.

 	Rules
Here is the encoding principle:

The input message consists of ASCII characters (7-bit)
The encoded output message consists of blocks of 0
A block is separated from another block by a space
Two consecutive blocks are used to produce a series of same value bits (only 1 or 0 values):
- First block: it is always 0 or 00. If it is 0, then the series contains 1, if not, it contains 0
- Second block: the number of 0 in this block is the number of bits in the series
 	Example
Let’s take a simple example with a message which consists of only one character: Capital C. C in binary is represented as 1000011, so with this method, this gives:

0 0 (the first series consists of only a single 1)
00 0000 (the second series consists of four 0)
0 00 (the third consists of two 1)
So C is coded as: 0 0 00 0000 0 00

 
Second example, we want to encode the message CC (i.e. the 14 bits 10000111000011) :

0 0 (one single 1)
00 0000 (four 0)
0 000 (three 1)
00 0000 (four 0)
0 00 (two 1)
So CC is coded as: 0 0 00 0000 0 000 00 0000 0 00

 	Game Input
Input
Line 1: the message consisting of N ASCII characters (without carriage return)
Output
The encoded message
Constraints
0 < N < 100
Example
Input
C
Output
0 0 00 0000 0 00

## Code

```js
/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/

const MESSAGE = readline();
const SEPARATOR = ' ';
const BIT_0 = '0';
const BIT_1 = '1';
// Write an answer using console.log()
// To debug: console.error('Debug messages...');

function not(bitString) {
    return bitString === BIT_0 ? BIT_1 : BIT_0;
}

// convert message to binary padding each char if needed to reach 7 bits per char.
let binaryMessage = MESSAGE.split('').reduce((accumulator,currentChar) => {
    let binaryChar = currentChar.charCodeAt(0).toString(2);
    let binaryCharLength = binaryChar.length;
    for (let i = 0; i < (7 - binaryCharLength); i++) {
        binaryChar = '0' + binaryChar;
    }
    return accumulator + binaryChar;
}, '');
// for each sequence of bits, generate unary blocks
let encodedSequence = '';
let index = 0
while(index > -1) {
    let digit = binaryMessage[index];
    let nextSequence = binaryMessage.indexOf(not(digit), index + 1);
    encodedSequence += digit === BIT_0 ? '00' : '0';
    encodedSequence += SEPARATOR;
    let sequenceLength = (nextSequence > -1 ? nextSequence : binaryMessage.length) - index;
    for(let i = 0; i < sequenceLength; i++) {
        encodedSequence += '0';
    }
    index = nextSequence;
    encodedSequence += index > - 1 ? SEPARATOR : '';
}

console.log(encodedSequence);
```


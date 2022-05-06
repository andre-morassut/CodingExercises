# Substitution Encoding

## Description

Level : easy

### Goal

You want to easily encode and decode messages with a simple and personalized method. To do so, you will use a substitution method.

The principle is simple, you have a comparison table like this one:
```
A B
C D
```
and a message to encode written with the characters available in your table:
```
CBA
```
You are going to take each of the characters that compose the message and replace them by its position in the table:
```
C => 10 (row 1 column 0)
B => 01 (row 0 column 1)
A => 00 (row 0 column 0)
```
The message becomes: `100100`

**Input**
```
Line 1: An integer rows for the number of rows of the table.
Lines 2 to rows + 1: A string for each row of the table. This string is composed of characters separated by one space.
Final line: The message to encode.
```

**Output**
```
Line 1: The encoded message.
```

**Constraints**
```
1 ≤ rows ≤ 10
```

**Example**

**Input**
```
2
A B
C D
CBA
```

**Output**
```
100100
```

## Code

```js
const rows = +readline();
const cache = new Map();
for (let i = 0; i < rows; i++) { // associative dictionary
    readline().split(' ').forEach((v, j) => cache.set(v, '' + i + j));
}
const message = [...readline()].map(v => cache.get(v)).join('');
console.log(message);
```


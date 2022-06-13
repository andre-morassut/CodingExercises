# Sum of Spiral's Diagonals

## Description

Level : easy

### Goal

Given a matrix of shape `N`×`N` arranged in a "spiral", with its numbers spiralling from `1` to `N²` inward, what is the sum of its diagonals? See examples to clarify what a spiral is.

**Example 1:**

The input: 3

Gives the following spiral:
```
1     2     3 
8     9     4
7     6     5
```
The sum of the diagonals is:
```
1 + 3 + 5 + 7 + 9 = 25
```

**Example 2:**

The input: 4

Gives the following spiral:
```
1    2      3     4
12   13    14     5
11   16    15     6
10   9      8     7
```
The sum of the diagonals is:
```
1 + 4 + 7 + 10 + 13 + 14 + 15 + 16 = 80
```
**Input**
```
N the number of layers of the spiral
```
**Output**
```
S the sum of the diagonals
```
**Constraints**
```
0 < N < 1500
0 < S < 2^32 - 1
```
**Example**

**Input**
```
5
```
**Output**
```
133
```

## Code

There are many ways to solve this exercise.

The one I chose rely on the following properties :
* Odd matrix : n² + (n² - 2) + (n² - 4) + (n² - 6) + [ 4 times substracting 4 ] + [ 4 times substracting 6 ] + [ 4 times substracting 8 ] and so on.
* Even matrix : n² + (n² - 1) + (n² - 1) + [ 4 times substracting 3 ] + [ 4 times substracting 5 ] + [ 4 times substracting 7 ] and so on.

So on an even matrix, the substraction will follow an odd pattern : 1, 3, 5, 7, ...

On an odd matrix, it will be an even pattern : 2, 4, 6, 8, ...

```js
let n = +readline();
let total = next = n ** 2;
let sub = n % 2 ? 2 : 1;
for (let i = 0; i < (sub + 2) && (next - sub) > 0; i++) {
    next = next - sub;
    total += next;
}
sub = sub + 2;
next = next - sub;
let i = 1;
while (next > 0) {
    if (i % 4 === 0) sub = sub + 2;
    i++;
    total += next;
    next = next - sub;
}
console.log(total);
```


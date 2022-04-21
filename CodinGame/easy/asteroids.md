# Asteroids

## Description

Level : easy

### Goal
You have been tasked with studying a region of space to detect potentially dangerous asteroids.

You are given two pictures of the night sky of dimensions W*H, taken at two different times t1 and t2.
For your convenience, asteroids have been marked with capital letters A to Z, the rest is empty space represented by a dot (.) .
Using the information contained in those two pictures, determine the position of the asteroids at t3, and output a picture of the same region of the sky.
If necessary, the final coordinates are to be rounded-down (floor).

Asteroids travel at different altitudes (with A being the closest and Z the farthest from your observation point) and therefore cannot collide with each other during their transit.
If two or more asteroids have the same final coordinates, output only the closest one.

It is guaranteed that all asteroids at t1 will still be present at t2, that no asteroids are hidden in the given pictures, and that there is only one asteroid per altitude.
NB: Because of the flooring operation, it is important that you choose a coordinate system with the origin at the top left corner and the y axis increasing in the downward direction.

**Input**
```
Line 1: five ints separated by a space, W H t1 t2 t3
Next H lines: a row of picture 1 and picture 2, separated by a white space.
```
**Output**
```
H lines for the state of the sky at t3
```
**Constraints**
```
0<W<=H<=20
0<=t1<t2<=t3<=10000
```
**Example**
```
Input
5 5 1 2 3
A.... .A...
..... .....
..... .....
..... .....
..... .....
Output
..A..
.....
.....
.....
.....
```
## Code

```js
// problem parameters & coord cache
let W, H, T1, T2, T3;
[W, H, T1, T2, T3] = [...readline().split(' ').map(v => +v)];
let asteroids = {};
// parse into coord cache
for (let i = 0; i < H; i++) {
    let line = [...readline()];
    for (let j = 0; j < line.length; j++) {
        if (line[j] !== '.' && line[j] != ' ') {
            if(!asteroids[line[j]]) {
                asteroids[line[j]] = [];
            }
            if (j > W) {
                asteroids[line[j]].push([j - (W + 1), i]);
            } else {
                asteroids[line[j]].unshift([j, i]);
            }
        }
    }
}
// init blank sky
let output = Array(H * W + H - 1).fill().map((v, i) => (i + 1) % (W+1) === 0 ? '\n' : '.').join('');
// ouput asteroids
let x, y, x1, x2, y1, y2, coords, indexInsert;
Object.keys(asteroids).sort().reverse().forEach((v, i) => {
    coords = asteroids[v];
    if (coords[0] && coords[1]) {
        [x1, y1] = coords[0];
        [x2, y2] = coords[1];
        x = Math.floor(x2 + ((x2 - x1) * ((T3 - T2) / (T2 - T1))));
        y = Math.floor(y2 + ((y2 - y1) * ((T3 - T2) / (T2 - T1))));
    } else if(coords[1]) {
        [x, y] = coords[1];
    }
    if (x >= 0 && x < W && y >= 0 && y < H) {
        indexInsert = (y * (W + 1)) + x;
        output = output.substring(0, indexInsert) + v + output.substring(indexInsert + 1);
    }
});
console.log(output);
```

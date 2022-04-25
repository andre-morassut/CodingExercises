# Rotating arrows

## Description

Level : easy

### Goal

A `W` x `H` grid is filled with arrows, each arrow will point to any one direction (UP, DOWN, RIGHT or LEFT).
You can know which direction the arrow is pointing to by knowing its ascii image,
`^`, `>`, `v`, `<` represent UP, RIGHT, DOWN and LEFT.

You can rotate an arrow clockwise, for example: ^ after rotation will become >.

After you rotate the arrow, the other arrow that the arrow is pointing at will start rotating clockwise too, this process continues until the last rotated arrow points back to the first arrow you rotate or the last rotated arrow points to the edge of the grid.

After you rotated the arrow at position (x, y), how many times of rotation will occur? (Index starts with 0)

For example:
```
W=2, H=2
x=0, y=0
```
Grid:
```
^>
<v
```
First we start at the arrow at position (0, 0), after rotating the arrow clockwise, the arrow now points to the right. New grid:
```
>>
<v
```
Now we rotate the arrow at (1, 0), and it will now point down, and we now rotate the arrow at (1, 1), and the arrow will point to the left. Next, we rotate the arrow at (0, 1), and the arrow will point to up, which is the arrow at (0, 0).

The arrow points back to the first arrow you rotate! So the result is 4, `4` rotation occurs!

**Input**
```
Line 1: Two integers W and H
Line 2: Two integers x and y
Next H lines: A line with W arrows represented by ascii char ^v<>
```

**Output**
```
The number of rotation times
```

**Constraints**
```
1 ≤ W, H ≤ 10
0 ≤ x < W
0 ≤ y < H
```

**Example**

**Input**
```
2 1
0 0
^v
```

**Output**
```
2
```

## Code

```js
let cache = {
    '^':[1, 0, '>'],
    '>':[0, 1, 'v'],
    'v':[-1, 0, '<'],
    '<':[0, -1, '^'],
}
let [w, h, xA, yA, x = xA, y = yA, res = 0] = (readline() + ' ' + readline()).split(' ').map(v => +v);
let map = Array(h).fill().map(v => readline().split(''));
do {
    [x, y] = visit(x, y);
    res++;
} while(x >= 0 && y >= 0 && x < w && y < h && (x !== xA || y !== yA))
console.log(res);

function visit(x, y) {
    let cached = cache[map[y][x]];
    map[y][x] = cached[2];
    return [x, y].map((v, i) => v + cached[i]);
}
```

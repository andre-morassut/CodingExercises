# Object Insertion

## Description

Level : easy

### Goal

You have an object to insert into a partially filled 2D grid.

You need to count the number of ways the object can fit into the empty areas of the grid.
If there is one and only one way, you also must display the grid with the inserted object.
Flips and rotations are NOT allowed on the object.

The object is represented as a series of strings, in which dots "." are empty areas and stars "*" are physical parts of the object.

Example:
```
*.
**
.*
```

The grid is provided in a similar fashion, dots "." are empty areas and number signs "#" are filled areas of the grid.

Notes:
- The representation of the object never presents empty rows or columns.
- The dimensions of the object are always less than or equal to the dimensions of the grid.

**Input**
```
First line: Two integers a and b separated by a space, denoting the numbers of rows and columns of the representation of the object.
Next a lines: Line of length b composed of the characters "." and "*".
Next line: Two integers c and d separated by a space, denoting the numbers of rows and columns of the grid.
Next c lines: Line of length d composed of the characters "." and "#".
```

**Output**
```
First line: Number of ways to insert the object in the grid.
If this number equals 1:
Next c lines: Line of length d composed of the characters ".", "#" and "*", showing grid state after object insertion.
```

**Constraints**
```
1 ≤ a ≤ c ≤ 10
1 ≤ b ≤ d ≤ 10
```

**Example**

**Input**
```
3 2
.*
**
.*
8 10
#..#######
#.##..####
###..##...
####.#####
##.#######
##......##
##.....###
########..
```

**Output**
```
1
#..#######
#.##*.####
###**##...
####*#####
##.#######
##......##
##.....###
########..
```

## Code

This algorithm slices the map to make its shape and area equal to the object, to create a sub map equal in size to the object.

If you replace the empty et occupied cells with 0 and 1 on the object, and with 1 and 0 on the sub map (inverse) - then when you substract the two matrices (`obj - map`), if no values in the resulting matrix is positive, it means the object fits in this portion of the map.

```js
let h, w, b, a, obj, map, xMax, yMax, result, xResult, yResult;
[b, a] = readline().split(' ');
obj = Array(+b).fill().map(v => [...readline().replaceAll('.', '0').replaceAll('*', '1')]);
[h, w] = readline().split(' ');
map = Array(+h).fill().map(v => [...readline().replaceAll('.', '1').replaceAll('#', '0')]);
xMax = w - a + 1;
yMax = h - b + 1;
result = 0;
for (let j = 0; j < yMax; j++) {
    for (let i = 0; i < xMax; i++) {
        let submap = map.slice(j, j + +b).map(v => v.slice(i, i + +a)).flat();
        let difmap = obj.flat().map((v, idx) => v - submap[idx]).filter(v => v > 0);
        if (difmap.length === 0) {
            result++;
            xResult = i;
            yResult = j;
        }
    }
}
if (result === 1) {
    obj.forEach((v, jj) => v.forEach((w, ii) => w == 1 ? map[jj + yResult][ii + xResult] = '*' : false));
    result += '\n' + map.map(v => v.join('').replaceAll('1', '.').replaceAll('0', '#')).join('\n');
}
console.log(result);
```


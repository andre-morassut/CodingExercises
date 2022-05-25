# The Mystic Rectangle

## Description

Level : easy

### Goal

Ataria lives on a toroidal map known as the Mystic Rectangle, where opposite edges of the map are connected. Crossing an edge teleports her to the opposite side. Ataria can move in any of the four cardinal directions or along the four diagonals of 45 degrees.

Given Ataria's coordinates and the coordinates of the goal, find the fastest time for her to reach the goal, assuming no obstacles.

* Moving East or West ±1 unit in x takes 0.3 seconds.
* Moving North or South ±1 unit in y takes 0.4 seconds.
* It takes 0.5 seconds to move diagonally, 1 unit East/West plus 1 unit North/South.

After travelling for 1 minute in any single cardinal direction (that is, 200 units East/West, or 150 units North/South), she ends up returning to the same place.

**Example**

Suppose Ataria starts near the top of the map and travels diagonally 15 units NorthEast and then straight 5 units due North. In doing so, she wraps around to the bottom of the map, arriving at the goal. Then at 9.5 seconds, this direct route makes the best time to the goal.

**Input**
```
Line 1: Two space separated integers x and y for the current position
Line 2: Two space separated integers u and v for the location of the goal
```

**Output**
```
Line 1: The decimal time to the goal in seconds, with precision of tenths
```

**Constraints**
```
0 ≤ x, u < 200
0 ≤ y, v < 150
```

**Example**

**Input**
```
50 15
65 145
```

**Output**
```
9.5
```

## Code

```js
const inputs = readline().split(' ').concat(readline().split(' '));
const x = +inputs[0], y = +inputs[1], u = +inputs[2], v = +inputs[3], a = 200, b = 150;

let minX = Math.min(Math.abs(u - x), Math.min(u, x) + (a - Math.max(u, x)));
let minY = Math.min(Math.abs(v - y), Math.min(v, y) + (b - Math.max(v, y)));
let time = (Math.min(minX, minY) * 0.5) + (Math.abs(minX - minY) * (minX < minY ? 0.4 : 0.3));
console.log(time.toFixed(1));
```


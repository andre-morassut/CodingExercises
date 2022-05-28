# Cosmic Love

## Description

Level : easy

### Goal

««Prompt»»
Gary is attracted to Alice. It is almost as if there is some mysterious force pulling them together. However, Alice is known for viciously tearing apart potential suitors that get too close. In fact, Alice is currently undergoing such a temper tantrum, and Gary must get away immediately lest he be torn asunder! Help Gary find the closest planet to land his spaceship on that will not be ripped apart by Alice's gravitational field.

««Details»»
N planets, including Alice, are listed with names name, radii r, masses m, and current distances c from Alice. The Roche Limit between a planet and Alice defines the distance below which a planet would disintegrate due to Alice's gravitational field. Determine the closest of the N planets that will not disintegrate.

««Math»»
Some equations reminiscent of high school physics:
    Alice's Roche Limit = rA * cube-root ( 2 * dA / dP )
        where rA is the radius of Alice,
        dA and dP are the densities of Alice and a planet.
    Volume of sphere V = 4/3 * pi * r^3
    Density d = m / V

Model each planet as a sphere of uniform density. Distances are measured between centers of the spheres. For simplicity's sake for defining the "closest" planet, assume that all celestial bodies are positioned in a line, with Alice and Gary at one end of the line.

««Disclaimer»»
This puzzle does not reflect reality and should be kept away from children under the age of 90. If you experience strange sensations of being ripped apart from within after solving this puzzle, call your doctor right away.
Input
Line 1: An integer N representing the number of planets, including Alice
Next N lines: Space separated strings name, r, m, and c, describing a planet.
    Radii and orbital distances are given in units of m
    Masses are given in units of kg
    Quantities are formatted in scientific notation: 0.00e00. For example, 8.00e3 represents 8,000, and 1.63e10 represents 16,300,000,000.
Output
The name of the closest planet to Alice that will remain intact
Constraints
2 ≤ N ≤ 30
1e0 ≤ r,m,c ≤ 1e50
1 ≤ length of a name ≤ 30
names consist of characters A-Za-z0-9_
Each test case has one unique solution
Example
Input
3
Alice 4.70e11 4.70e42 0
BLARGHHH 6.30e09 1.30e31 5.14e11
G7_24a 4.49e08 2.50e30 5.51e13
Output
G7_24a

## Code

_Warning : the following algorithm fails at the additional validators, but the details are not available. Obviously, this is a rounding issue and hopefully I'll find time to iron it out._

```js
const N = +readline(); // number of planets
let inputs = Array(N).fill().map(v => readline().split(' ')).sort((a, b) => a[3] - b[3]) // [name, r, m, c]
let densities = inputs.map(v => +v[2] / (4/3 * Math.PI * (+v[1])**3)); // [d]
let dlim = densities.map((v, i) => inputs[i][3] - (inputs[0][1] * Math.cbrt(2 * densities[0] / v))); // dlim = [c - roche]
let closest = dlim.reduce((acc, cur, i, arr) => (cur > 0 && cur < acc) ? cur : acc, Number.MAX_SAFE_INTEGER); // min dlim
console.log(inputs[dlim.indexOf(closest)][0]); // name at min dlim index
```


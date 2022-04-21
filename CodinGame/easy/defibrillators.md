# Defibrillators

## Description

Level : easy

### Goal
The city of Montpellier has equipped its streets with defibrillators to help save victims of cardiac arrests. The data corresponding to the position of all defibrillators is available online.

Based on the data we provide in the tests, write a program that will allow users to find the defibrillator nearest to their location using their mobile phone.

#### Rules
The input data you require for your program is provided in text format.
This data is comprised of lines, each of which represents a defibrillator. Each defibrillator is represented by the following fields:
```
A number identifying the defibrillator
Name
Address
Contact Phone number
Longitude (degrees)
Latitude (degrees)
These fields are separated by a semicolon (;).
```
__Beware: the decimal numbers use the comma (,) as decimal separator. Remember to turn the comma (,) into dot (.) if necessary in order to use the data in your program.__
 
### DISTANCE
The distance d between two points A and B will be calculated using the following formula:

```
x = (longitudeB - longitudeA) * cos ((latitudeA + latitudeB) / 2)
y = (latitudeB - latitudeA)
d = √(x² + y²) * 6371
```

__​Note: In this formula, the latitudes and longitudes are expressed in radians. 6371 corresponds to the radius of the earth in km.__

The program will display the name of the defibrillator located the closest to the user’s position. This position is given as input to the program.
### Game Input

**Input**
```
Line 1: User's longitude (in degrees)
Line 2: User's latitude (in degrees)
Line 3: The number N of defibrillators located in the streets of Montpellier
N next lines: a description of each defibrillator
```

**Output**
```
The name of the defibrillator located the closest to the user’s position.
```

**Constraints**
```
0 < N < 10000
Example
Input
3,879483
43,608177
3
1;Maison de la Prevention Sante;6 rue Maguelone 340000 Montpellier;;3,87952263361082;43,6071285339217
2;Hotel de Ville;1 place Georges Freche 34267 Montpellier;;3,89652239197876;43,5987299452849
3;Zoo de Lunaret;50 avenue Agropolis 34090 Mtp;;3,87388031141133;43,6395872778854
```

**Output**
```
Maison de la Prevention Sante
```

## Code

```js
/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/

const LON = strToRad(readline());
const LAT = strToRad(readline());
const N = parseInt(readline());

// Process: transform input data into [name, distance] array of defib data
let defibrillators = [];
let defibrillator;
for (let i = 0; i < N; i++) {
    defibrillator = getDefibValues(readline());
    defibrillators.push(defibrillator);
}
// reduce to minimum distance
let answer = defibrillators.reduce((prev, cur) => !prev || (cur[1] < prev[1]) ? cur : prev);
console.log(answer[0]);

function strToRad(degreeWithComma) {
    return degreeWithComma.replace(',', '.') * Math.PI / 180;
}

function findDistance(lonA, latA, lonB, latB) {
    let x = (lonB - lonA) * Math.cos((latA + latB) / 2);
    let y = latB - latA;
    return (Math.sqrt(x**2 + y**2) * 6371).toPrecision(8);
}

function getDefibValues(DEFIB) {
    let defibValues = DEFIB.split(';');
    return [defibValues[1], findDistance(LON, LAT, strToRad(defibValues[4]), strToRad(defibValues[5]))];
}
```


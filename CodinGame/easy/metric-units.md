# Metric Units

## Description

Level : easy

### Goal

The goal of this exercise is to add two lengths with given metric units. To calculate it properly you first need to convert them to the same unit. Present the result using the smaller unit.

For instance:
```
4cm + 2dm
```
must convert `2dm` to `20cm`:
```
4cm + 20cm
```
it then results to:
```
24cm
```
If you like to challenge yourself a little more...
Try to limit the number of ifs and switches as much as possible in your code.

**Input**
```
Line 1: the expression to calculate valueunit+valueunit
```
**Output**
```
valueunit
```
`value` should be a sum of two given values after units conversion to the smaller one.

`unit` should be the smaller unit of the two parameters.

**Constraints**
```
value is a real number:
0 <= value <= 1000
with precision <= 0.00001

unit can be one of the following:
- um (micrometer)
- mm (millimeter) where 1mm = 1000um
- cm (centimeter) where 1cm = 10mm
- dm (decimeter) where 1dm = 10cm
- m (meter) where 1m = 10dm
- km (kilometer) where 1km = 1000m
```
**Example**

**Input**
```
1m + 1cm
```
**Output**
```
101cm
```

## Code

```js
const units = ['um', '', '', 'mm', 'cm', 'dm', 'm', '', '', 'km'];
let decomp = [...readline().matchAll(/^([\d]+[\.|\,]?[\d]*)(um|mm|cm|dm|m|km){1}\s*\+{1}\s*([\d]+[\.|\,]?[\d]*)(um|m|cm|mm|dm|km){1}$/gm)][0];
let iOp1 = units.indexOf(decomp[2]);
let iOp2 = units.indexOf(decomp[4]);
let indMin = Math.min(iOp1, iOp2);
let [iMinVal, iMaxVal] = indMin === iOp1 ? [1, 3] : [3, 1];
let conv = Math.abs(iOp1 - iOp2);
let add = ((decomp[iMaxVal] * (10 ** conv)) + +decomp[iMinVal]);

console.log((Math.round(add * 10000) / 10000) + units[indMin]);
```

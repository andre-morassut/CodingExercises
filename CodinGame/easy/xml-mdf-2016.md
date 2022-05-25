# XML MDF-2016

## Description

Level : easy

### Goal

In this challenge, a data format that is a simplified version of XML is used. Tags are identified by a lowercase letter. A start tag is represented by that single letter, and the closing tag is represented by the `"-"` character, followed by that letter.

For example, the string `"ab-bcd-d-c-ae-e"` is the equivalent of `<a> <b> </ b> <c> <d> </ d> </ c> </a> <e> </ e>` in XML. The supplied string will always be properly formed.

Now we define the depth of a tag as 1 + the number of tags in which it is nested.

In the previous example:
* a and e have a depth of 1,
* b and c have a depth of 2
* and d has a depth of 3.

The weight of a tag name is defined as the sum of the reciprocals of the depths of each of its occurrences.

For example, in the chain a-abab-b-a-b, there are:
* Two tags a with depths of 1 and 2
* Two tags b with depths of 1 and 3.

thus the weight of a is (1/1) + (1/2) = 1.5 and the weight of b is (1/1) + (1/3) = 1.33.

In this challenge you must determine the letter of the tag with the greatest weight in the string argument.

**Input**
```
On a single line, a properly formed string of at most 1024 characters representing nested tags.
```

**Output**
```
The letter corresponding to greatest weight tag name. If two tag names have the same weight, display the smallest in alphabetical order.
```

**Example**

**Input**
```
aa-aa-a-a
```

**Output**
```
a
```

## Code

Solution - with an array to implicitly store characters value (first position is the level, others are chars : 1 for a, 2 for b and so on).

```js
let tags = readline().match(/-?[a-z]/gm).reduce((acc, cur) => {
    if (cur.length === 1) { // opening tag => update weight
        acc[0]++;
        acc[cur.charCodeAt(0) - 96] += 1/acc[0];
    } else {
        acc[0]--;
    }
    return acc;
}, Array(27).fill(0)).slice(1);
let answer = tags.reduce((acc, cur, i, arr) => cur > arr[acc] ? i : acc, 0); // first strict maximum is the answer
console.log(String.fromCharCode(answer + 97));
```

Another solution - with a map this time.

```js
let vMax = 0;
let cMax;
const sequence = readline().match(/-?[a-z]/gm);
let weights = sequence.reduce((acc, cur, i, arr) => { // compute weight by letter
    if (cur.length === 1) {
        acc.level++;
        if (!acc.map.has(cur)) {
            acc.map.set(cur, 0);
        }
        acc.map.set(cur, acc.map.get(cur) + 1/acc.level);
    } else {
        acc.level--;
    }
    return acc;
}, {level:1,map:new Map()});
weights.map.forEach((v, c) => { // find the max value with the min letter
    if (v > vMax) {
        vMax = v;
        cMax = c;        
    } else if (v === vMax) {
        if (!cMax) {
            cMax = c;
        } else if (c < cMax) {
            cMax = c;
        }
    }
});
console.log(cMax);
```

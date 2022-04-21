#  1D Spreadsheet

## Description

Level : easy

### Goal
You are given a 1-dimensional spreadsheet. You are to resolve the formulae and give the value of all its cells.

Each input cell's content is provided as an operation with two operands arg1 and arg2.

There are 4 types of operations:
* `VALUE arg1 arg2` : The cell's value is arg1, (arg2 is not used and will be "_" to aid parsing).
* `ADD arg1 arg2` : The cell's value is arg1 + arg2.
* `SUB arg1 arg2` : The cell's value is arg1 - arg2.
* `MULT arg1 arg2` : The cell's value is arg1 × arg2.

Arguments can be of two types:

* Reference $ref: If an argument starts with a dollar sign, it is a interpreted as a reference and its value is equal to the value of the cell by that number ref, 0-indexed.

For example, "$0" will have the value of the result of the first cell.
Note that a cell can reference a cell after itself!

* Value val: If an argument is a pure number, its value is val.
For example: "3" will have the value 3.

There won't be any cyclic references: a cell that reference itself or a cell that references it, directly or indirectly.

**Input**
```
Line 1: An integer N for the number of cells.
Next N lines: operation arg1 arg2
operation is one of { VALUE, ADD, SUB, MULT }
arg1 and arg2 are either a number ("-?[0-9]+"), a reference ("\$[0-9]+") or nothing "_".
```

**Output**

N lines: the value of each cell, one value per line, from cell 0 to cell N

**Constraints**
```
1 ≤ N ≤ 100
-10000 ≤ val ≤ 10000
$0 ≤ $ref ≤ $(N-1)
val ∈ ℤ
ref ∈ ℕ
There are no cyclic references.
```
**Example**

**Input**
```
2
VALUE 3 _
ADD $0 4
```

**Output**
```
3
7
```
## Code

```js
/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/

let cache = {};

// parse inputs as object list
operations = Array(+readline()).fill().map(() => {
    let inputs = readline().split(' ');
    return {operation: inputs[0], arg1: inputs[1], arg2: inputs[2], toString(){
        return `${this.operation}-${this.arg1}-${this.arg2}`;
    }};
});

// compute sequentially the cells
operations.map((op) => {
    console.log(calcOperationWithRef(op));
});

// recursive function to resolve references
function calcOperationWithRef(operation) {
    if (cache[operation]) {
        return cache[operation];
    }
    // arg1
    if (operation.arg1.toString().startsWith('$')) {
        operation.arg1 = calcOperationWithRef(operations[operation.arg1.substring(1)]);
    }
    // arg2
    if (operation.arg2.toString().startsWith('$')) {
        operation.arg2 = calcOperationWithRef(operations[operation.arg2.substring(1)]);
    }
    cache[operation] = calcOperation(operation);
    return cache[operation];
}

// Performs operation when no ref are present
function calcOperation(operation) {
    // Nb. The "+ 0" prevents results being "-0"
    switch(operation.operation) {
        case 'VALUE':
            result = 0 + +operation.arg1;
            break;
        case 'ADD':
            result = 0 + +operation.arg1 + +operation.arg2;
            break;
        case 'SUB':
            result = 0 + +operation.arg1 - +operation.arg2;
            break;
        case 'MULT':
            result = 0 + +operation.arg1 * +operation.arg2;
            break;
        default:
            result = 'ERR!';
            break;
    }
    return result; 
}
```


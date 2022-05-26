# Feature Extraction

## Description

Level : easy

### Goal

**Convolution** is a method for extracting features from an input image which can be used for training a Deep Neural Network to classify input image. It produces an output matrix where each element is a weighted sum of neighbouring input elements using a kernel (weight matrix).

Given an input image of size `r × c` pixels (each pixel represented by an integer) and a kernel of size `m × n`, print the `(r-m+1) × (c-n+1)` output pixels after the convolution.

To calculate the output pixel values, place the top left corner of kernel of size `m × n` on the input image matrix starting from the top left corner and then shift it one step right as long as it fits in the input image matrix. Then start again on the next row down.

At each location, calculate the sum of the weights multiplied by the pixel values at the overlapped cells.

**Example how convolution works**

```
Image Pixel Matrix

a11 a12 a13 a14
a21 a22 a23 a24
a31 a32 a33 a34
a41 a42 a43 a44

Kernel Weight Matrix

w11 w12
w21 w22

In this case we have 9 possible placements of the kernel matrix. Output image size is 3×3.

Top left corner at (0,0)
Weighted Sum = a11 * w11 + a12 * w12 + a21 * w21 + a22 * w22

Top left corner at (0,1)
Weighted Sum = a12 * w11 + a13 * w12 + a22 * w21 + a23 * w22

Top left corner at (0,2)
Weighted Sum = a13 * w11 + a14 * w12 + a23 * w21 + a24 * w22

Top left corner at (1,0)
Weighted Sum = a21 * w11 + a22 * w12 + a31 * w21 + a32 * w22

Top left corner at (1,1)
Weighted Sum = a22 * w11 + a23 * w12 + a32 * w21 + a33 * w22

So on...
```

For an animated visualization please refer to this link: https://tinyurl.com/nk0vnyel

Resources for more information:
* https://d2l.ai/chapter_convolutional-neural-networks/conv-layer.html
* https://developers.google.com/machine-learning/practica/image-classification/convolutional-neural-networks

**Input**
```
Line 1: The height (r) and width (c) of input image matrix separated by space.
Next r lines: c pixel values separated by spaces.
Line r+2: The height (m) and width (n) of the kernel matrix separated by space.
Next m lines: n weights separated by spaces.
```

**Output**
```
Print the output image matrix after the convolution.
```

**Constraints**
```
Kernel matrix is a square matrix.
m ≤ r and n ≤ c
```

**Example**

**Input**
```
3 3
100 200 100
200 100 200
50 100 50
2 2
-1 1
1 -1
```

**Output**
```
200 -200
-150 150
```

## Code

```js
let [r, c] = readline().split(' ');
let image = Array(+r).fill().map(v => readline().split(' '));

let [m, n] = readline().split(' ');
let kernel = Array(+m).fill().map(v => readline().split(' '));

let target = Array(r - m + 1).fill().map((_, j) =>
    Array(c - n + 1).fill().map((_, i) => 
        kernel.reduce((sumRow, rowVal, row) => sumRow + 
            rowVal.reduce((sumCol, colVal, col) => 
               sumCol + (colVal * image[j + row][i + col])
            , 0)
        , 0)
    ) 
);

console.log(target.map(v => v.join(' ')).join('\n'));
```

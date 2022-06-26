# Decode the message

## Description

Level : easy

### Goal

As an FBI agent you intercepted a message from terrorists. This message has to be decrypted, and to do so you have access to 2 pieces of information : `P` and `C`.

`C` is the alphabet used to write the message, and contains all the letters/characters needed to decode it.

`P` corresponds to the encoded value of the message.

Thankfully, you happen to know how this value is computed, and now need to reverse the following process :
* Assuming the alphabet is 'abcd', each letter is associated to its index : a = 0, b = 1, c = 2, d = 3.
* For the following values, a new letter is either added or switched :
* aa = 4, ba = 5, ca = 6, da = 7
* ab = 8, bb = 9, cb = 10, db = 11
* ...
* aaa = 20, baa = 21, caa = 22, daa = 23, and so on.
* The whole message gets a unique value this way. For example with a full alphabet (26 letters) 'hello' would be 7073801.

Get it done agent ! (Good Luck)

## Code

P is a summation of `n` terms (with `n` being the length of the message and the alphabet index starting at 0) as follows:
```
P = (alphabet index of letter 1)
    + ( ( (letter 2 index) + 1 ) * alphabet size^1 )
    + ...
    + ( ( (letter n index) + 1 ) * alphabet size^(n - 1) )
```

So, decoding P is done using:
```
DECODED = index letter 1 = (P % alphabet size) ; 
          index letter 2 = (P / (alphabet size - 1)) ;
          ...
          index letter n = ( P / ( (alphabet size - 1)^(n - 1) ) )
```

Variant 1

```js
let decoded = '';
let message = +readline();
let alphabet = readline();
while (message >= 0) {
    decoded += alphabet.charAt(message % alphabet.length);
    message = message / alphabet.length - 1;
}
console.log(decoded);
```

Variant 2 - With an array as alphabet

```js
const P = +readline();
const C = [...readline()];
let decoded = '';
let message = P;
while (message >= 0) {
    decoded += C[(message % C.length) | 0];
    message = message / C.length - 1;
}
console.log(decoded);
```

An encode function.
```js
function encode(message) {
    let c = "abcd";
    let acc = [...message].reduce((ac, cur, i) => ac += c.indexOf(cur) + (i > 0 ? c.length ** i : 0), 0);
    console.error('encode: ' + message + ' = ' + acc);
}
```

A decode function.
```js
function decode(mess, alpha) {
    let res = '';
    while (mess >= 0) {
        res += alpha.charAt(mess % alpha.length);
        mess = mess / alpha.length - 1;
    }
    console.error('decode: ' + mess + ' = '  + res);
}
```

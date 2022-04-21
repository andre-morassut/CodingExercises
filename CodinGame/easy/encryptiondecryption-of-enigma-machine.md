# Encryption/Decryption of Enigma Machine

## Description

Level : easy

### Goal
During World War II, the Germans were using an encryption code called Enigma – which was basically an encryption machine that encrypted messages for transmission. The Enigma code went many years unbroken. Here's How the basic machine works:

First Caesar shift is applied using an incrementing number:
If String is AAA and starting number is 4 then output will be EFG.

> A + 4 = E
> A + 4 + 1 = F
> A + 4 + 1 + 1 = G

Now map EFG to first ROTOR such as:

> ABCDEFGHIJKLMNOPQRSTUVWXYZ

> BDFHJLCPRTXVZNYEIWGAKMUSQO

So EFG becomes JLC. Then it is passed through 2 more rotors to get the final value.

If the second ROTOR is AJDKSIRUXBLHWTMCQGZNPYFVOE, we apply the substitution step again thus:

> ABCDEFGHIJKLMNOPQRSTUVWXYZ

> AJDKSIRUXBLHWTMCQGZNPYFVOE

So JLC becomes BHD.

If the third ROTOR is EKMFLGDQVZNTOWYHXUSPAIBRCJ, then the final substitution is:

> ABCDEFGHIJKLMNOPQRSTUVWXYZ

> EKMFLGDQVZNTOWYHXUSPAIBRCJ

So BHD becomes KQF.

Final output is sent via Radio Transmitter.

**Input**
```
Line 1: ENCODE or DECODE
Line 2: Starting shift N
Lines 3-5:
BDFHJLCPRTXVZNYEIWGAKMUSQO ROTOR I
AJDKSIRUXBLHWTMCQGZNPYFVOE ROTOR II
EKMFLGDQVZNTOWYHXUSPAIBRCJ ROTOR III
Line 6: Message to Encode or Decode
```

**Output**
```
Encoded or Decoded String
Constraints
0 ≤ N < 26
Message consists only of uppercase letters (A-Z)
1 ≤ Message length < 50
```

**Example**

**Input**

```
ENCODE
4
BDFHJLCPRTXVZNYEIWGAKMUSQO
AJDKSIRUXBLHWTMCQGZNPYFVOE
EKMFLGDQVZNTOWYHXUSPAIBRCJ
AAA
```

**Output**
```
KQF
```
## Code

```js
const rotors = [];
let output;

/**
 * Auto-generated code below aims at helping you parse
 * the standard input according to the problem statement.
 **/
const operation = readline(); 
let pseudoRandomNumber = parseInt(readline());
for (let i = 0; i < 3; i++) {
    const rotor = readline();
    rotors.push(Array.from(rotor));
}
let message = readline();

// Write an answer using console.log()
// To debug: console.error('Debug messages...');

if (operation == 'ENCODE') {
    // ceasar shift if encode
    let input = caesarShift(Array.from(message), pseudoRandomNumber);
    // rotor transformation
    output = input.map(token => {
        let encodedToken = token;
        for(let i = 0; i < rotors.length; i++) {
            encodedToken = (rotors[i])[encodedToken.charCodeAt(0) - 65];
        }
        return encodedToken;
    });
} else {
    // rotor decode
    input = Array.from(message).map(token => {
        let decodedToken = token;
        for(let i = rotors.length - 1; i >= 0; i--) {
            decodedToken = String.fromCharCode((rotors[i]).indexOf(decodedToken) + 65);
        }
        return decodedToken;
    });
    // caesar unshit
    output = caesarShift(input, -pseudoRandomNumber);
}
// output solution
console.log(output.join(''));
// ---------------------------------------------------------------------
// FUNCTIONS
// ---------------------------------------------------------------------
function caesarShift(message, shift) {
    return message.map((token, index) => {
        let char = token.charCodeAt(0) - 65;
        char += shift > 0 ? shift + index : shift - index;
        char = mod(char, 26) + 65;
        return String.fromCharCode(char);
    });
}

// if the first operator of the % operation is negative
// then JS returns the incorrect modulo according to the 
// mathematical definition and adding the second operator 
// corrects it.
// See https://fr.wikipedia.org/wiki/Modulo_(op%C3%A9ration)
function mod(i, n) {
    return ((i % n) + n) % n;
}
```


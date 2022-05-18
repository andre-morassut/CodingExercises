# Caesar is the chief

## Description

Level : easy

### Goal

During the galactic war against the Zorglons, the Earth Intelligence Agency intercepted a lot of messages.

It is your task to decode them.

You know that :
1. The messages are always in capital letter. Words are separated with white spaces. You don't have to decode these spaces.
2. They are coded with a caesar cypher.
3. The Zorglons always include the word "**CHIEF**" in them to be sure there are true messages. Be careful, this must be a separated word : a message such as "**HANDKERCHIEF**" is not a true message.

Note that the caesar cipher is a shift in the alphabet : for example, with a right shift of 3, A becomes D, B becomes E ... and Z becomes C (cf. https://en.wikipedia.org/wiki/Caesar_cipher).

Given a message, you must decode it (i.e. find the correct shift and output the text containing the word "CHIEF") or output "WRONG MESSAGE" if it is not a true message.

**Input**
```
Ligne 1 One string to decode
```

**Output**
```
Ligne 1 One decoded string or "WRONG MESSAGE"
```

**Example**

**Input**
```
HELLO
```

**Output**
```
WRONG MESSAGE
```

## Code

Functional.

```js
const pattern = /(?:(?:^.*\s+)|^)CHIEF(?:(?:\s+.*$)|$)/gm;
let msg = readline();
let rots = Array(26).fill(msg).map((v, i) => shift(v, i))
let valid = rots.findIndex(v => v.match(pattern) !== null)
console.log(valid > -1 ? rots[valid] : 'WRONG MESSAGE');

function shift(msg, n) {
    return [...msg].map(v => v >= 'A' && v <= 'Z' ? 
    String.fromCharCode((((v.charCodeAt(0) - 65) + n) % 26) + 65) : v)
    .join('');
}
```

Procedural.

```js
const pattern = /(?:(?:^.*\s+)|^)CHIEF(?:(?:\s+.*$)|$)/gm;
let msg = readline();
let decoded = msg.match(pattern) !== null;
let rot = 0;;
while (!decoded && rot < 25) {
    msg = shift(msg, 1);
    if (msg.match(pattern) !== null) {
        decoded = true;   
    } else {
        rot++;
    }
}

function shift(msg, n) {
    return [...msg].map(v => 
        v >= 'A' && v <= 'Z' ? 
        String.fromCharCode((((v.charCodeAt(0) - 65) + n) % 26) + 65) : 
            v
    ).join('');
}

console.log(decoded ? msg : 'WRONG MESSAGE');
```

The functional approach is more elegant, whereas the procedural one seems easier to read.

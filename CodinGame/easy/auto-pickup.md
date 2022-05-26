# Auto pickup

## Description

Level : easy

### Goal

You have been looking on the network `packet` a game is sending, and you have been thinking about making a system to automatically pick things up for you!

You have found the `packet` is one big string of binary data of instructions.

Each instruction is formatted in this way:

`[instruction id (3 bits)][packet length (4 bits)][packet info (packet length bits)].`

What you need to do is extract the item drop instructions, they have id 101, and their `packet` info is the item id you will need! This id might be different lengths, so look at the `packet` length.

What you need to send back is a set of pickup instructions, id 001. Remember the `packet` length!

`001[item id length][item id]`

For example: "10100010101001011" we have the id and length:

"101 0001 0101001011" which means we should take 1 bit for the item id, so
"101 0001 0".

Then we look at the rest of the packet
"101001011" and split that up into "101 0010 11" and get the second id "11".

Then we just send the response "001 0001 0" and "001 0010 11".

**Input**
```
Line 1: the length of the packet
Line 2: the packet to inspect
```

**Output**
```
Line 1: The packet you send to the game to pick up your items
The ids should be sent in the order they were found in the input packet
```

**Constraints**
```
There will always be at least one item drop
```

**Example**

**Input**
```
9
101001010
```

**Output**
```
001001010
```

## Code

```js
readline(); //n is not necessary

function analyzePacket(p) {
    if (p && p.length > 7) {        
        let packetLen = p.substring(3,7);
        let restIndex = 7 + parseInt(packetLen, 2);
        let rest = p.substring(restIndex);
        if (p.substring(0, 3) === '101') {
            let info = p.substring(7, restIndex);
            return '001' + 
            info.length.toString(2).padStart(4, '0') +
            info + analyzePacket(rest);
        } else {
            return analyzePacket(rest);
        }
    } else {
        return '';
    }
}

console.log(analyzePacket(readline()));
```

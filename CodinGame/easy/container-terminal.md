
# Container Terminal

## Description

Level : easy

### Goal



## Code

```js
const N = +readline();
for (let i = 0; i < N; i++) {
    const stacksTop = [...readline()].reduce((prev, cur) => {
        if (prev.indexOf(cur) == -1) {
            let okStack = prev.find(v => v.charCodeAt(0) > cur.charCodeAt(0));
            if (okStack) {
                prev[prev.indexOf(okStack)] = cur;
            } else {
                prev.push(cur);
            }
        }
        return prev;
    }, []);
    console.log(stacksTop.length);
}
```

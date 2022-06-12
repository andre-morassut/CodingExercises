# Monday Tuesday Happy Days

## Description

Level : easy

### Goal

Given a start date with a known week day, your program must compute the day of the week at another date anytime in the same year.

**Input**
* __Line 1:__ whether or not the year is a leap year: 1 if it is, 0 otherwise. A leap year is a year when February has 29 days instead of 28. The actual year itself is not given.
* __Line 2:__ the initial date formatted as day of the week abbreviated month day in month, e.g. Monday Apr 23 for April 23rd.
* __Line 3:__ the date you must give the day of the week for, formatted as abbreviated month day in month, e.g. Apr 24 for April 24th.

The abbreviated month names are `Jan`, `Feb`, `Mar`, `Apr`, `May`, `Jun`, `Jul`, `Aug`, `Sep`, `Oct`, `Nov` and `Dec`.

**Output**

* __Line 1:__ The day of the week for the second date: Monday, Tuesday, Wednesday, Thursday, Friday, Saturday or Sunday.

**Constraints**
```
Both dates are always within the same year.
Both dates are valid—there is no Jan 45, Feb 29 on non-leap years, etc.
The second date may be before the first one.
```
**Example**

**Input**
```
0
Monday Jan 1
Jan 2
```
**Output**
```
Tuesday
```

## Code

I'm not really happy with this solution. I saw others used the Date API, which is logical. 
I wanted to avoid using it to produce a concise solution working only with simple data. But the result feels clumsy. Maybe I'll work out a better solution in the future.

```js
const leap = +readline();
const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
const monthNames   = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
const monthLengths = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
monthLengths[1] += leap; // leap year ?

let [sourceDayOfWeek, sourceMonth, sourceDayOfMonth] = readline().split(' ');
sourceDayOfMonth = +sourceDayOfMonth;

let [targetMonth, targetDayOfMonth] = readline().split(' ');
targetDayOfMonth = +targetDayOfMonth;

let indexStartMonth = monthNames.indexOf(sourceMonth);
let indexEndMonth = monthNames.indexOf(targetMonth);

let answer;
if (indexStartMonth === indexEndMonth) {
    answer = targetDayOfMonth - sourceDayOfMonth;
} else if (indexStartMonth < indexEndMonth) {
    answer = monthLengths[indexStartMonth] - sourceDayOfMonth;
    answer += monthLengths.slice(indexStartMonth + 1, indexEndMonth).reduce((ac, cur) => ac += cur, 0);
    answer += targetDayOfMonth;
} else {
    answer = sourceDayOfMonth;
    answer += monthLengths.slice(indexEndMonth + 1, indexStartMonth).reduce((ac, cur) => ac += cur, 0);
    answer += monthLengths[indexEndMonth] - targetDayOfMonth;
    answer = monthLengths.reduce((ac, v) => ac += v, 0) - answer - (leap ? 2 : 1);
}
answer = (dayNames.indexOf(sourceDayOfWeek) + answer) % 7

console.log(dayNames[answer]);
```


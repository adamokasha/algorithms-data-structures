# FizzBuzz

An game that logs to the console numbers 1 through n. For multiples of three log "fizz" instead, for multiples of five log "buzz" and for multiples of three and five log "fizzbuzz". Otherwise, log the numbers.

### Overview

Loop n many times. At each loop use the modulo operator to check what should be printed given the current number.

### Code

```javascript
function fizzBuzz(n) {
  for (let i = 1; i <= n; i++) {
    if (i % 3 === 0 && i % 5 === 0) {
      console.log("fizzbuzz");
    } else if (i % 3 === 0) {
      console.log("fizz");
    } else if (i % 5 === 0) {
      console.log("buzz");
    } else {
      console.log(i);
    }
  }
}
```

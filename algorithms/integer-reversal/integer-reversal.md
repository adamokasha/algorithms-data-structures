# Integer Reversal

Reverses an integer.

### Overview

Convert the number to a string. We can then call split on the string so that we can reverse the resulting array. Finally by joining the array, we will have a _string_ representation of our input integer in reverse. We can then use the built-in `parseInt` method to return an integer.

**Note**: In order for this to work with a negative number, we need to use `Math.sign(n)`.

### Code

```javascript
function reverseInt(n) {
  const reversed = n
    .toString()
    .split("")
    .reverse()
    .join("");

  return parseInt(reversed) * Math.sign(n);
}
```

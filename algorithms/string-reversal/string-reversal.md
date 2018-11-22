# String Reversal

Reverses a string.

### Implementation Overview

Create an empty string to build up. Iterate over the input string from the beginning, adding each character currently being iterated over before the string being built.

### Code

```javascript
function reverse(str) {
  let reversed = "";

  for (let character of str) {
    reversed = character + reversed;
  }

  return reversed;
}
```

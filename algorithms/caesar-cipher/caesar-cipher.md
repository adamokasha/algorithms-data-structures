# Caesar Cipher

The Caesar cipher is a simple cipher which encrypts a string by shifting the character over by `n`, alphabetically. For example, `abc -> cde` is a Caesar cipher that where the shift value is `n = 2`.

### Overview

Create an array of letters. Use a lower case duplicate of the string passed in and loop over ever letter in the string to be encrypted.

If the index when we shift is greater than the length of our array of letters (25 for zero based array in this case), subtract by 26 to get the index of the letter to add to the encrypted string.

If it is less (ie. a negative number) add 26 to get the index of the letter to add to the encrypted string.

Several edge cases to account for:

- Uppercase letters
  - Check current character against original string to see if it is uppercase. If so, make it uppercase and add to shifted string.
- A `n` parameter than is outside the range of length of letters in the alphabet (such as 100).
  - Use the modulo operator

### Code

```javascript
function cesarCipher(str, num) {
  num = num % 26;
  const strLower = str.toLowerCase();
  const lettersArr = "abcdefghijklmnopqrstuvwxyz".split("");
  let shifted = "";

  for (let i = 0; i < strLower.length; i++) {
    if (str[i] === " ") {
      shifted = shifted + " ";
      continue;
    }

    let startingIndex = lettersArr.indexOf(strLower[i]);
    let shiftedIndex = startingIndex + num;

    if (shiftedIndex > 25) shiftedIndex = shiftedIndex - 26;
    if (shiftedIndex < 0) shiftedIndex = 26 + shiftedIndex;
    if (str[i] === str[i].toUpperCase()) {
      shifted += lettersArr[shiftedIndex].toUpperCase();
    } else {
      shifted += lettersArr[shiftedIndex];
    }
  }
  return shifted;
}
```

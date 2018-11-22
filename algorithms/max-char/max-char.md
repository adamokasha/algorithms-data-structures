# Max Character

Find the most common character in a given string.

### Overview

Populate a character map with each character in the string as a key and the number of its occurences as the value.

Loop over the character map to find the most common character.

### Code

```javascript
function maxChar(str) {
  const charMap = {};
  let currentMax = 0;
  let maxChar = "";

  for (let char of str) {
    charMap[char] = ++charMap[char] || 1;
  }

  for (let char in charMap) {
    if (charMap[char] > currentMax) {
      currentMax = charMap[char];
      maxChar = char;
    }
  }

  return maxChar;
}
```

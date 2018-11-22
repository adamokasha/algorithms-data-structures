# Palindromes

Checks if a given string is a palindrome. Palindromes are words that, when reversed, form the same word.

## Overview

Ignoring special characters and spaces, split the string and reduce. Check if the original string is equal to the accumulated string.

## Code

```javascript
function palindrome(str) {
  const reversed = str.split("").reduce((rev, char) => (rev = char + rev), "");

  return str === reversed;
}
```

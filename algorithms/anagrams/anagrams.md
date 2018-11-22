# Anagrams

Checks if two strings are anagrams of each other. Two words are said to be anagrams of one another if they have the same characters in the same frequency.

**Note**: Special characters are ignored and the algorithm is executed case-insensitively.

### Overview

Build a character map for each string. If they don't have the same number of keys (chars), return false.

Loop over each character in one of the character maps. Compare the same keys/value pairs and return false if any comparison is false. Return true otherwise.

### Code

```javascript
function anagrams(stringA, stringB) {
  const aCharMap = buildCharMap(stringA);
  const bCharMap = buildCharMap(stringB);

  if (Object.keys(aCharMap).length !== Object.keys(bCharMap).length) {
    return false;
  }

  for (let char in aCharMap) {
    if (aCharMap[char] !== bCharMap[char]) {
      return false;
    }
  }

  return true;
}

function buildCharMap(str) {
  const charMap = {};

  for (let char of str.replace(/[^\w]/g, "").toLowerCase()) {
    charMap[char] = charMap[char] + 1 || 1;
  }

  return charMap;
}
```

### Alternative

```javascript
function anagrams(stringA, stringB) {
  return cleanString(stringA) === cleanString(stringB);
}

function cleanString(str) {
  return str
    .replace(/[^\w]/g, "")
    .toLowerCase()
    .split("")
    .sort()
    .join("");
}
```

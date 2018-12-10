# Harmless Ransom Note

An algorithm based on the idea of cutting words out of a magazine to create a (harmless) ransom note.

### Overview

Assume no special characters and only lowercase letters.

Create a word map out of the magazine text. Set the possibility of making a ransom note to be true (in a variable) initially.

Loop over every word and if a word is not found in the magazine text character map or it has been depleted, set the validity to false.

Return the variable that tracks if ransom note is valid.

### Code

```javascript
function harmlessRansomNote(note, text) {
  const textMap = buildWordMap(text);
  const noteArr = note.trim().split(" ");
  let isValid = true;

  for (let word of noteArr) {
    if (!textMap[word]) {
      isValid = false;
      break;
    }
    textMap[word]--;
  }
  return isValid;
}

function buildWordMap(str) {
  const wordMap = {};
  const strArr = str.split(" ");
  for (let char of strArr) {
    wordMap[char] = wordMap[char] + 1 || 1;
  }
  return wordMap;
}
```

### Big O

#### Time Complexity

| Best | Average | Worst |
| :--: | :-----: | :---: |
| O(n) |  O(n)   | O(n)  |

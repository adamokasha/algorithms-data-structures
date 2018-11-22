# Array Chunking

Given an array and a chunk size, return a new array made up of array chunks of the original array. The last chunk can be less than the given chunk size.

### Overview

Loop over the entire array. At each loop push a slice of the original array into a new array. Move the slice over by the given size of the chunk.

### Code

```javascript
function chunk(array, size) {
  const chunked = [];
  let index = 0;

  while (index < array.length) {
    chunked.push(array.slice(index, index + size));
    index += size;
  }

  return chunked;
}
```

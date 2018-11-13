# Selection Sort

## Description

As the name implies, selection sort works by selecting an item in the list and comparing it to another item and making a swap if the items are ordered incorrectly.

## Implementation

### Overview

Create an outer loop that loops from the beginning to the end of an array. Create a variable inside to act as the current _selection_ and set it to the current index (i). We can call it min.

Create an inner loop whose index (j) starts at the next item from the first loop till the end of the array. Here, compare the _values_ of the item at the selection index (min) to that of the item in this inner loop. If the inner loop item is smaller set min to the _index_ of the inner loop item (j). Next, while still in the inner loop, do a swap if min now does not equal the outer loop index.

Once booth loops have finished, return the array.

### Pseudocode

- Create a swapping function
- Create an outer loop that start from the beginning and loops till the end of the array.
  - Set `min = i`
- Create an inner loop that whose starting condition is `j = i + 1` and loops till the end of the array.
  - Check if `arr[j] < arr[min]`. In other words, compare the next item (j) to the _selection_.
    - If true, set `min = j`
  * If `min !== i`, then swap the elements.

* Return the array.

### Code

```javascript
function swap(arr, i, j) {
  let temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}

function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let min = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) {
        min = j;
      }
    }
    if (min !== i) {
      swap(arr, i, min);
    }
  }
  return arr;
}
```

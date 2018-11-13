# Selection Sort

## Description

As the name implies, selection sort works by selecting an item in the list and comparing it to another item and making a swap if the items are ordered incorrectly. Unlike bubble sort, selection sort works by sorting the smallest items into position first.

## Implementation

### Overview

Begin by setting the first item as the smallest item. Check the next item and see if its smaller. If so, set it as the smallest item. If the smallest item is not what it was when we began, swap the two items.

### Pseudocode

- Create a swapping function
- Create an outer loop that start from the beginning and loops till the end of the array.
  - Set `min = i`. This will let `i` act as our current `selection`
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

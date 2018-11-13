# Insertion Sort

## Description

Sorts a list by creating a left _sorted_ segment and inserting items from the right _unsorted_ segment.

## Implementation

### Overview

Create an the outer loop to sort through the unsorted segment. Start this loop at the second element since the first element, by itself, is always sorted. Capture the current element's value.

Create an inner loop that starts at the end of the sorted segment and works backwards towards its start. Use this loop to insert the element in the correct spot by shifting all the elements right of the insertion point over by one (thereby creating a slot to insert). Finally, insert the current element's value.

### Pseudocode

- Create three variables:
  - `value`: to compare an unsorted element with elements in the sorted segment
  - `i`: to iterate over the unsorted segment
  - `j`: to iterate over the sorted segment
- Create an outer loop starting from the second position of the array to loop over the unsegmented section
  - Set `value` to be that of the element at the current index to save it (we will be shifting elements around later).
  - Create an inner loop to compare `value` with elements in the sorted segment
    - Shift each element that is greater one element over: `arr[j + 1] = arr[j]`
  - Insert the current element's value at one position over from where the inner loop broke: `arr[j + 1] = value`. This is the insertion point.
- Return the array.

### Code

```javascript
function insertionSort(arr) {
  let value, i, j;

  for (i = 1; i < arr.length; i++) {
    value = arr[i];
    for (j = i - 1; j >= 0 && arr[j] > value; j--) {
      arr[j + 1] = arr[j];
    }
    arr[j + 1] = value;
  }
  return arr;
}
```

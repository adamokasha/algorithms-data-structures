# Linear Search

Searches an array for a specified value.

## Implementation Overview

Create a loop that checks over every item in the array for the specified value. If found, returns index where element was found, else returns -1.

### Code

```javascript
function linearSearch(arr, val) {
  for (let i = 0; i < arr.length; i++) {
    if (val === arr[i]) {
      return i;
    }
  }
  return -1;
}
```

### Big O

#### Time Complexity

| Best | Average | Worst |
| :--: | :-----: | :---: |
| O(1) |  O(n)   | O(n)  |

# Binary Search

Uses a divide and conquer approach by choosing the element in the middle and shrinking the searching window to the left or right based on that middle point being smaller or greater than the value being searched. **Only works on a sorted array**.

### Implementation Overview

Starting with the left and right pointers at both ends of the array, set the a variable to be the middle element between them.

If the value we're searching for is smaller than the middle element, then move the left pointer one element past the middle.

If the value we're searching for is greater than the middle element, then move the right pointer one element past the middle.

If the middle is equal to the value, then the array contains that value. Return the middle variable tracking the index. Otherwise return -1.

### Code

```javascript
function binarySearch(arr, val) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    let middle = Math.floor((left + right) / 2);
    if (arr[middle] === val) return middle;
    if (arr[middle] < val) left = middle + 1;
    if (arr[middle] > val) right = middle - 1;
  }
  return -1;
}
```

### Big O

#### Time Complexity

| Best | Average  |  Worst   |
| :--: | :------: | :------: |
| O(1) | O(log n) | O(log n) |

# Binary Heap

## What is a Binary Heap?

Binary heaps are a form of a binary tree that come in two varieties:

- A max binary heap where parent nodes are always greater than their child nodes.
- A min binary heap where parent nodes are always smaller than their child nodes.

Although parent nodes are always greater or smaller than their child nodes, siblings are not ordered.

Binary heaps are typically used to implement priority queues.

**Important Note**: The implementation that follows is that of a max binary heap, although it can easily be addapted to be a min binary heap.

## The Binary Heap Class

```javascript
class MaxBinaryHeap {
  constructor() {
    this.values = [];
  }
}
```

## Adding Methods

### Insert Method

#### Description

Inserts a node at the end of the tree and "bubbles up" its position until it is correctly placed (if required at all). Returns the tree.

#### Implementation Overview

Push the value to the values array. Starting from the end of the array, loop to the beginning. At every loop, check if the current element is smaller than or equal the parent element, then stop, else swap the parent element with the child element to let it "bubble up". Repeat with the child element's new position.

Note that the parent index is always equal to the current index - 1 / 2, _floored_.

#### Pseudocode

- Push the inserted value into the tree
- Initialize an `index` for this value at its current position, the end of the array
- Create a variable `element` equal to the value of the element at index
- Loop while index is greater than 0
  - Create variable `parentIndex` which is equal to `Math.floor((index - 1) / 2)`
  - Create a variable `parent` and set to the element at `parentIndex`
  - If `element <= parent`, then break (the element cannot bubble up further)
  - Swap
    - Swap the element at `parentIndex` with `element`
    - Swap the element at `index` with `parent`
  - Set `index = parentIndex` fro the next loop

#### Code

```javascript
  insert(val) {
    this.values.push(val);
    let index = this.values.length - 1;
    const element = this.values[index];
    while (index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      let parent = this.values[parentIndex];
      if (element <= parent) break;
      this.values[parentIndex] = element;
      this.values[index] = parent;
      index = parentIndex;
    }
    return this.values;
  }
```

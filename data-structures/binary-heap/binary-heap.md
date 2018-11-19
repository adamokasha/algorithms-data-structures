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

### Extract Max

#### Description

Removes the maximum value from the tree and re-sorts the tree. Returns the removed element.

#### Implementation Overview

The implementation requires a "sink down" approach. This means that we will first swap the root node with the last item in the tree. This old root node will then be popped off.

The new root will be sunk down until it reaches it correct position in the tree. To sink an element down, we need to compare it to its left and right children and sink it below the larger child element of the two _only if_ they are larger than that element (the parent). This process should repeat until parent is greater or equal to both its children.

Note:

- Left child index, if it exists within the boundary of the tree, is equal to: `2 * parentIndex + 1`
- Right child index, if it exists within the boundary of the tree, is equal to: `2 * parentIndex + 2`

#### Pseudocode

- Create a variable to save the first item in the tree called `min`
- Create a variable to save the last item in the tree called `end`
- If `this.values.length > 0`
  - Swap the first item in the tree with `end`
  - Use a sinkDown helper function
    - Start at an `index` of 0, and with `element` value at that index
    - Create `leftChildIndex` and `rightChildIndex`
    - Initiate `leftChild` and `rightChild`
    - Create a `swap` variable to determine what to swap, set initially at `null`
    - If the `leftChildIndex < length` (ie. within bounds)
      - Give `leftChild` the value at `leftChildIndex` in the tree
      - If `leftChild`'s value is greater than the `element`'s, then set `swap` as `leftChildIndex`
    - If the `rightChildIndex < length` (ie. within bounds)
      - Give `rightChild` the value at `rightChildIndex` in the tree
      - If `swap === null` and the `rightChild`'s value is greater than `element`'s **OR** if `swap !== null` and `rightChild`'s value is greater than `leftChild`'s
        - Set `swap` to `rightChildIndex`
    - If `swap === null`, element doesn't need to sink further, break the loop.
    - Swap the value at `index` with that at `swap`
    - Set `index` to `swap` for the next loop

#### Code

```javascript
  extractMax() {
    const min = this.values[0];
    const end = this.values.pop();
    if (this.values.length > 0) {
      this.values[0] = end;
      this.bubbleUp();
    }
    return min;
  }
  bubbleUp() {
    let index = 0;
    const length = this.values.length;
    const element = this.values[0];
    while (true) {
      let leftChildIndex = 2 * index + 1;
      let rightChildIndex = 2 * index + 2;
      let leftChild, rightChild;
      let swap = null;

      if (leftChildIndex < length) {
        leftChild = this.values[leftChildIndex];
        if (leftChild > element) {
          swap = leftChildIndex;
        }
      }
      if (rightChildIndex < length) {
        rightChild = this.values[rightChildIndex];
        if (
          (swap === null && rightChild > element) ||
          (swap !== null && rightChild > leftChild)
        ) {
          swap = rightChildIndex;
        }
      }
      if (swap === null) break;
      this.values[index] = this.values[swap];
      this.values[swap] = element;
      index = swap;
    }
  }
```

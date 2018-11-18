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

- Check if the tree has any values. If not return `undefined`
- Check if the tree has only one value. If so return the that single value.
- Create a swap helper function
- Swap the first element (the root) and the last element
- Pop the old root off the tree and save it in a variable `oldRoot`
- Create a `parentIndex` variable and set to 0
- Start a Loop
  - Create and set the required variables:
    - Create a `leftChildIndex` variable and set to `2 * parentIndex + 1` or `null` if outside of the values array's boundary.
    - Create a `righChildIndex` variable and set to `2 * parentIndex + 1` or `null` if outside of the values array's boundary.
    - Create a `parent` variable set to element at `parentIndex`
    - Create a `leftChild` variable set to the element at `leftChildIndex` if it exists or `null`
    - Create a `rightChild` variable set to the element at `rightChildIndex` if it exists or `null`
  - If the parent is greater than or equal to both the `leftChild` and `rightChild`. If true, then break because the element has "sunk" to the correct spot.
  - Else
    - Find the index of the larger child `largerChildIndex`
    - Swap the parent with the larger child
    - Set `parent = largerChildIndex`
- Return `oldRoot`

#### Code

```javascript
  extractMax() {
    if (!this.values.length) return undefined;
    if (this.values.length === 1) return this.values.pop();

    function swap(arr, i, j) {
      let temp = arr[i];
      arr[i] = arr[j];
      arr[j] = temp;
    }

    swap(this.values, 0, this.values.length - 1);
    const oldRoot = this.values.pop();
    let parentIndex = 0;

    while (true) {
      if (!this.values.length) return undefined;
      const leftChildIndex =
          2 * parentIndex + 1 <= this.values.length - 1
            ? 2 * parentIndex + 1
            : null,
        rightChildIndex =
          2 * parentIndex + 2 <= this.values.length - 1
            ? 2 * parentIndex + 2
            : null,
        parent = this.values[parentIndex],
        leftChild = leftChildIndex ? this.values[leftChildIndex] : null,
        rightChild = rightChildIndex ? this.values[rightChildIndex] : null;

      if (parent >= leftChild && parent >= rightChild) break;

      const largerChildIndex =
        leftChild > rightChild ? leftChildIndex : rightChildIndex;
      swap(this.values, parentIndex, largerChildIndex);
      parentIndex = largerChildIndex;
    }
    return oldRoot;
  }
```

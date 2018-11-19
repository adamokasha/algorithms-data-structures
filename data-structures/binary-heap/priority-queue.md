# Priority Queue

## What is a Priority Queue?

A priority queue is a data structure where each element has a priority and where each element is served in order of their priority (highest first).

**Important Note**: This implementation of the priority queue will be done with a _min binary heap_.

## The Node Class

```javascript
class Node {
  constructor(val, priority) {
    this.val = val;
    this.priority = priority;
  }
}
```

## The Binary Heap Class

```javascript
class PriorityQueue {
  constructor() {
    this.values = [];
  }
}
```

## Adding Methods

### Enqueue Method

#### Description

Inserts a node at the end of the tree and "bubbles up" its position until it is correctly placed (if required at all). Returns the tree.

#### Implementation Overview

Push the value to the values array. Starting from the end of the array, loop to the beginning.
At every loop, check if the current element's priority is greater than or equal the parent element's priority. If it is, then stop, else swap the parent element with the child element to let it "bubble up". Repeat with the child element's new position.

**Important Note**: In this example, a _lower number indicates a higher priority_.

Note that the parent index is always equal to the current index - 1 / 2, _floored_.

#### Pseudocode

- Create a new node `newNode`
- Push the node into the tree
- Initialize an `index` for this node at its current position, the end of the array
- Create a variable `element` equal to the value of the element at index
- Loop while index is greater than 0
  - Create variable `parentIndex` which is equal to `Math.floor((index - 1) / 2)`
  - Create a variable `parent` and set to the element at `parentIndex`
  - If `element.priority <= parent.priority`, then break (the element cannot bubble up further)
  - Swap
    - Swap the element at `parentIndex` with `element`
    - Swap the element at `index` with `parent`
  - Set `index = parentIndex` for the next loop
  - Return the values.

#### Code

```javascript
  enqueue(val, priority) {
    let newNode = new Node(val, priority);
    this.values.push(newNode);
    let index = this.values.length - 1;
    const element = this.values[index];
    while (index > 0) {
      let parentIndex = Math.floor((index - 1) / 2);
      let parent = this.values[parentIndex];
      if (element.priority >= parent.priority) break;
      this.values[parentIndex] = element;
      this.values[index] = parent;
      index = parentIndex;
    }
    return this.values;
  }
```

### Dequeue

#### Description

Removes the maximum priority value from the tree and re-sorts the tree. Returns the removed element.

#### Implementation Overview

The implementation requires a "sink down" approach. This means that we will first swap the root node with the last item in the tree. This old root node will then be popped off.

The new root will be sunk down until it reaches it correct position in the tree. To sink an element down, we need to compare it's priority with of its left and right children's priorities' and sink it below the higher priority child element of the two _only if_ they are larger than that element (the parent). This process should repeat until parent is greater or equal to both its children.

Note:

- Left child index, if it exists within the bounds of the tree, is equal to: `2 * parentIndex + 1`
- Right child index, if it exists within the bounds of the tree, is equal to: `2 * parentIndex + 2`

#### Pseudocode

**Note**: In a min binary heap, we assume that a lower priority _value_ means a higher priority.

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
      - If `leftChild`'s priority is higher than the `element`'s priority, then set `swap` as `leftChildIndex`
    - If the `rightChildIndex < length` (ie. within bounds)
      - Give `rightChild` the value at `rightChildIndex` in the tree
      - If `swap === null` and the `rightChild`'s priority is higher than `element`'s **OR** if `swap !== null` and `rightChild`'s priority is higher than `leftChild`'s
        - Set `swap` to `rightChildIndex`
    - If `swap === null`, element doesn't need to sink further, break the loop.
    - Swap the value at `index` with that at `swap`
    - Set `index` to `swap` for the next loop

#### Code

```javascript
  dequeue() {
    const min = this.values[0];
    const end = this.values.pop();
    if (this.values.length > 0) {
      this.values[0] = end;
      this.sinkDown();
    }
    return min;
  }
  sinkDown() {
    let idx = 0;
    const length = this.values.length;
    const element = this.values[0];
    while (true) {
      let leftChildIdx = 2 * idx + 1;
      let rightChildIdx = 2 * idx + 2;
      let leftChild, rightChild;
      let swap = null;

      if (leftChildIdx < length) {
        leftChild = this.values[leftChildIdx];
        if (leftChild.priority < element.priority) {
          swap = leftChildIdx;
        }
      }
      if (rightChildIdx < length) {
        rightChild = this.values[rightChildIdx];
        if (
          (swap === null && rightChild.priority < element.priority) ||
          (swap !== null && rightChild.priority < leftChild.priority)
        ) {
          swap = rightChildIdx;
        }
      }
      if (swap === null) break;
      this.values[idx] = this.values[swap];
      this.values[swap] = element;
      idx = swap;
    }
  }
```

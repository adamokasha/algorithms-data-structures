# Stack

## What is a Stack?

A stack is a collection of objects that follows a LIFO (last in first out) model for adding and removing items.

### Creating the Node Class

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}
```

### Creating the Stack Class

```javascript
class Stack {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
}
```

## Adding Methods

### Push Method

#### Description

Adds an item to the end of the stack. Returns the size of the stack.

Note that we are pushing to the _beginning_ of the stack to avoid traversing to the end and increasing time complexity from O(1) to O(n).

#### Implementation Overview

Create a new node. If the stack does not have a node at the first property, then set first and last as the new node. Otherwise set the new node as the first and link the old first item to be new first.

#### Pseudocode

- Create a new node
- If there is no node at stack's `first` property
  - Set the `first` and `last` properties of the stack as the new node
- Else
  - Store the current first in a `temp` variable
  - Set the `first` property of the stack to be the new node
  - Set new node's `next` to the `temp` variable
- Return incremented size.

#### Code

```javascript
  push(val) {
    let newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      let temp = this.first;
      this.first = newNode;
      newNode.next = temp;
    }
    return ++this.size;
  }
```

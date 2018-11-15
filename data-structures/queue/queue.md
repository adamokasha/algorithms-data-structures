# Queue

## What is a Queue?

A queue is a collection that follows a FIFO (first in first out) model for adding and removing items.

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
class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
}
```

## Adding Methods

### Enqueue Method

A push-like method to add a node to the queue. Returns the queue's size.

Note that we are adding to the end (last property) so that we can get queue-like behaviour when dequeuing (shifting).

#### Implementation Overview

Create a new node. Set the queue's last node's next property to be the new node. Set the node node to be the queue's last property.

#### Pseudocode

- Create a new node
- If a first node does not exists in the queue
  - Set the first and last property of the queue to the new node
- Else
  - Set the `this.last.next` to be the new node
  - Set `this.last` to be the new node
- Return the incremented size.

#### Code

```javascript
  enqueue(val){
    const newNode = new Node(val);
    if(!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    return ++this.size;
  }
```

### Dequeue Method

A shift-like method to remove the first item in the queue. Returns the value of the queue.

#### Implementation Overview

Save the current first item in the list to a variable. Set the first item to now be the first item's next property.

#### Pseudocode

- If a first node does not exist in the queue, then return null.
- Create a new `temp` variable and set it to the queue's current first property
- If the queue's first property is equal to the last (Only one item in the queue)
  - Set last to null
- Set first to be the first's next property
- Decrement size
- Return the value of the item removed from the queue.

#### Code

```javascript
  dequeue(){
    if(!this.first) return null;
    let temp = this.first;
    if(this.first === this.last) {
      this.last = null;
    }
    this.first = this.first.next;
    this.size--;
    return temp.val;
  }
```

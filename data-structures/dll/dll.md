# Doubly Linked List

## What is a Doubly linked list?

A DLL is a data structure consisting of a sequence of nodes (objects) that have a a _two way_ link to other nodes.

They have a head, tail and length property.

![Doubly Linked List](dll_1.jpg)

## Creating the Node Class

```javascript
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
    this.prev = null;
  }
}
```

## Creating the Doubly Linked List Class

```javascript
class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
}
```

## Adding Methods

### Push Method

Adds a new node to the end of the list. Returns the list.

#### Implementation Overview

If no tail exists set, tail to newly created node. If a tail already exists, sets the tail to be the newly created node.

#### Pseudocode

- Create a new node.
- If no tail exists in the list, then it is empty. Set the head and tail to be the new node.
- Else
  - Set the current tail to be the new tail
  - Set the new node's `prev` property to be the current tail
  - Set the tail to be the new node.
- Increment length
- Return the list.

#### Code

```javascript
  push(val) {
    const newNode = new Node(val);
    if (!this.tail) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
      this.tail = newNode;
    }
    this.length++
    return this;
  }
```

### Pop Method

Removes the node at the end of the list. Returns the removed node.

#### Implementation Overview

Set the second to last item as the tail. Sever the link to the list of the old tail.

#### Pseudocode

- If no tail exists in the list, then it is empty. Return undefined.
- Save the old tail to a variable.
- If `list.length === 1`
  - Set head and tail to null
- Else
  - Set the tail to be the the old tail's prev property
  - Set that new tail's next property to be null to sever its link to the old tail
  - Set the old tails prev property to null to sever its link to the list
- Increment length
- Return the old tail.

#### Code

```javascript
  pop() {
    if (!this.tail) return undefined;
    let oldTail = this.tail;
    if (this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.tail = oldTail.prev;
      this.tail.next = null;
      oldTail.prev = null;
    }
    this.length--;
    return oldTail;
  }

```

### Shift Method

Removes the node at the start of the list. Returns the removed node.

#### Implementation Overview

Set the second to first item as the head. Sever the link of the new head to the old and the old head to the list.

#### Pseudocode

- If no head exists, then the list is empty. Return undefined.
- Save the old head in a variable.
- If `list.length === 1`
  - Set head and tail to null
- Else
  - Set the head to be the old tail's next property
  - Set the new head's prev property to null
  - Set the old head's next property to null
- Decrement length
- Return the old head.

#### Code

```javascript
  shift() {
    if (!this.head) return undefined;
    let oldHead = this.head;
    if (this.length === 1) {
      this.head = null;
      this.tail = null;
    } else {
      this.head = oldHead.next;
      this.head.prev = null;
      oldHead.next = null;
    }
    this.length--;
    return oldHead;
  }
```

### Unshift Method

Add a node at the start of the list. Returns the list.

#### Implementation Overview

Create a new node. Check if a head property exists on the list. If not set the head and tail to the new node. Otherwise, set the prev property of the old head to be new node, connect the new node to the current head and finally, set the head to be the new node.

#### Pseudocode

- Create a new node.
- If no head exists
  - set `this.head` and `this.tail` to the new node
- Else
  - Set the prev property of the head to be the new node
  - Set the next property of the new node to be the head
  - Set the head to be the new node
- Increment length
- Return the list.

#### Code

```javascript
  unshift(val) {
    let newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.head.prev = newNode;
      newNode.next = this.head;
      this.head = newNode;
    }
    this.length++;
    return this;
  }
```

### Get Method

Returns the node at a given index.

#### Note on SLL vs DLL Get Methods

Unlike with a Singly Linked List, we can optimize a DLL's get method due to the two way link between nodes. Since we can now start at the tail and traverse backwards, time complexity can be greatly reduced if we are retrieving a node that is situated near the end of the list.

#### Implementation Overview

First, find the mid point between the head and tail.

If the index is smaller than the mid point, traverse forwards starting from the head.

If the index is larger than the mid point, traverse backwards starting from the tail.

#### Pseudocode

- If the `index` is smaller than zero or greater than `length - 1`, then the `index` is in an invalid range. Return undefined.
- If `index` is 0 return the head.
- If `index` is equal to `length - 1`, return the tail
- Find the mid point between the head and tail
- Initiate and `i` and a `node` variable
- If index is smaller than the mid point
  - Set `node` to `this.head` and traverse forward
- Else
  - Set `node` to `this.tail` and traverse backwards
- Return the node.

#### Code

```javascript
  get(index) {
    if (index < 0 || index > this.length - 1) return undefined;
    if (index === 0) return this.head;
    if (index === this.length - 1) return this.tail;
    let middle = Math.floor(this.length / 2);
    let node;
    let i;
    if (index < middle) {
      node = this.head;
      for (i = 0; i < index; i++) {
        node = node.next;
      }
    } else {
      node = this.tail;
      for (i = this.length - 1; i > index; i--) {
        node = node.prev;
      }
    }
    return node;
  }
```

### Set Method

Sets the value at a given node. Return a boolean.

#### Implementation Overview

Use the get method to return the node at the given index. If a node is found, then set the new value and return false. Otherwise return false.

#### Pseudocode

- Create a `node` variable and set it to the return value of calling `this.get` with the given `index`.
- If a `node` is found, then update its value and return true
- Else return false.

#### Code

```javascript
  set(index, val) {
    let node = this.get(index);
    if (node) {
      node.val = val;
      return true;
    }
    return false;
  }
```

### Insert Method

Inserts a node at a given index. Returns a boolean.

#### Implementation Overview

Create a new node node. First, Connect the node previous to the new node's insertion index to the new node. Then, connect the node node next to the new node insertion index to the new node.

#### Pseudocode

- If index is smaller than zero or greater than length, then return false
- If index is equal to zero use the unshift method.
- If index is equal to `this.length` use the push method.
- Create a new node.
- Save the next and previous nodes to variables.
- Attach the new node to the previous node.
  - Set the prev node's next property to be the new node.
  - Set the new node's prev property to be the previous node.
- Attach the new node to the next node
  - Set the new node's next property to be the next node
  - set the next node's prev property to be the new node
- Increment length
- Return true.

#### Code

```javascript
  insert (index, val) {
    if(index < 0 || index > this.length) return false;
    if(index === 0) return !!this.unshift(val);
    if(index === this.length) return !!this.push(val);
    let newNode = new Node(val);
    let prevNode = this.get(index - 1);
    let nextNode = prevNode.next;

    prevNode.next = newNode;
    newNode.prev = prevNode;

    newNode.next = nextNode;
    nextNode.prev = newNode;

    this.length++;
    return true;
  }
```

### Remove Method

Removes the node at the given index. Returns the removed node.

#### Implementation Overview

First, sever the link of the removed node to the node previous to it. Then attach that previous node to the node after the removed node. Finally sever the links of the removed node to the list.

#### Pseudocode

- If index is less than zero or greater than `this.length - 1` return false
- If index is equal to zero use the shift method
- If index is equal to `this.length` use the pop method.
- Create variables for the removed node, the previous node and the next node (node next to the removed node)
- Set the previous node's `next` property to the next node
- Set the next node's `prev` property to be the previous node
- Set the removed node's `next` and `prev` properties to `null`
- Decrement length
- Return the removed node.

#### Code

```javascript
  remove (index) {
    if(index < 0 || index > this.length - 1) return false;
    if (index === 0) return !!this.shift();
    if(index === this.length - 1) return !!this.pop();
    let removedNode = this.get(index);
    let prevNode = removedNode.prev;
    let nextNode = removedNode.next;

    prevNode.next = nextNode;
    nextNode.prev = prevNode;

    removedNode.prev = null;
    removedNode.next = null;

    this.length--;
    return removedNode;
  }

```

# Hash Table

## What is a Hash Table?

A hash table is a data structure consisting of a collection of key-value pairs. Hashing the keys via a _hash function_ should derive an index of where the key/value pair can be found.

A good hash function should:

- Provide uniform distribution of hash values to minimize collision.
- Be deterministic, meaning that for any input to the hash function we should receive the same output
- We can use two strategies to mitigate a hash function returning the same index for two or more keys:
  - Seperate chaining: creates a "bucket" at the index and stores the key/value pairs in it
  - Linear probing: moves to the next index if an index is already "occupied"

JavaScript already has hash table implementation via `Objects` and `Maps`. For the purpose of understanding how hash tables work a very simple hash table will be implemented here.

**Note**: This implementation will use _seperate chaining_ to mitigate same indices for different keys.

## Creating the Hash Table Class

```javascript
class HashTable {
  constructor(size = 53) {
    this.keyMap = new Array(size);
  }
}
```

## Creating the Hash Function

This simple hash function uses a prime number, character encoding and the modulo operator to derive an index.

```javascript
  _hash(key) {
    let total = 0;
    let PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      let char = key[i];
      let value = char.charCodeAt(0) - 96;
      total = (total * PRIME + value) % this.keyMap.length;
    }
    return total;
  }
```

## Adding Methods

### Set Method

#### Description

Sets the key/value pair at the index derived from the hashing function.

#### Implementation Overview

First get the index by using the hash function. Then check if the index in the table is empty. If it is, create a bucket there (an empty array). Insert the key/value pair in the bucket.

#### Code

```javascript
  set(key, value) {
    const index = this._hash(key);
    if (!this.keyMap[index]) {
      this.keyMap[index] = [];
    }
    this.keyMap[index].push([key, value])
  }
```

### Get Method

Retrieves the specified key from the hash table.

#### Implementation Overview

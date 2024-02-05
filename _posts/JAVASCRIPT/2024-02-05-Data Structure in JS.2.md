---
layout: post
title: "2024-02-05-Data Structures in JS -Linked List- "
categories: [Javascript]
---


# Data Structures in JS

 This post is about 2 data structures in JS that I learned. 

## Linked List
A linked list is a chained data structure. Each node consists of two pieces of information: the data of the node and the pointer to the next node. Linked list and conventional array are both linear data structures with serialized storage.

### Difference from array

#### Linked List

- **Memory Allocation**
Elements in a linked list are scattered throughout memory.
Each element points to the next one in the sequence.

- **Dynamic Size**
Easily accommodates a dynamic size.
Adding or removing elements is more efficient than arrays.

- **Access Time**
Accessing an element requires traversing the list from the beginning, resulting in O(n) time complexity for access.

- **Memory Efficiency**
Uses memory efficiently for dynamic data sizes.
No need to preallocate memory for a fixed size.

- **Insertion/Deletion**
Efficient for frequent insertions and deletions.
Adding or removing elements involves updating pointers.

#### Array
- **Memory Allocation**
Elements in an array are stored in contiguous memory locations.

- **Fixed Size**
Generally has a fixed size when created.
Resizing an array might involve creating a new one and copying elements.

- **Access Time**
Direct access to elements using an index, resulting in O(1) time complexity for access.

- **Memory Efficiency**
Less memory-efficient for dynamic sizes.
Might lead to unused allocated space if the array is resized.

- **Insertion/Deletion**
Less efficient for frequent insertions and deletions, especially in the middle.
Shifting elements is required when inserting or deleting in the middle.

#### Use Cases

- **Linked List**
Suitable for scenarios with dynamic sizes and frequent insertions and deletions.
When memory needs to be allocated and deallocated efficiently.

- **Array**
Ideal for scenarios where direct access to elements by index is important.
When the size is known in advance, and efficient random access is required.

### Method of linked list in javascript

- **size**: Return the number of node(s).
- **head**: Return the element of the head.
- **add**: Add another node in the tail.
- **remove**: Remove a certain node.
- **indexOf**: Return the index of a node.
- **elementAt**: Return the node of an index.
- **addAt**: Insert a node at a specific index.
- **removeAt**: Delete a node at a specific index.

```
class Node {
  // Node constructor with data and optional next parameter
  constructor(data, next = null) {
    this.data = data;
    this.next = next;
  }
}

class LinkedList {
  // LinkedList constructor with head initialized to null
  constructor() {
    this.head = null;
  }

  // Return the number of node(s) in the linked list
  size() {
    let count = 0;
    let current = this.head;
    while (current) {
      count++;
      current = current.next;
    }
    return count;
  }

  // Return the element of the head (first node)
  head() {
    return this.head ? this.head.data : null;
  }

  // Add another node at the tail of the linked list
  add(data) {
    const newNode = new Node(data);
    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
  }

  // Remove a node with a certain data value
  remove(data) {
    if (!this.head) {
      return;
    }
    if (this.head.data === data) {
      this.head = this.head.next;
      return;
    }
    let current = this.head;
    let prev = null;
    while (current && current.data !== data) {
      prev = current;
      current = current.next;
    }
    if (!current) {
      return;
    }
    prev.next = current.next;
  }

  // Return the index of a node with a certain data value
  indexOf(data) {
    let index = 0;
    let current = this.head;
    while (current) {
      if (current.data === data) {
        return index;
      }
      current = current.next;
      index++;
    }
    return -1; // Return -1 if the value is not found
  }

  // Return the node at a specific index
  elementAt(index) {
    if (index < 0) {
      return null;
    }
    let count = 0;
    let current = this.head;
    while (current) {
      if (count === index) {
        return current;
      }
      current = current.next;
      count++;
    }
    return null; // Return null if the index exceeds the size of the list
  }

  // Insert a node at a specific index
  addAt(index, data) {
    if (index < 0) {
      return;
    }
    const newNode = new Node(data);
    if (index === 0) {
      newNode.next = this.head;
      this.head = newNode;
      return;
    }
    let count = 0;
    let current = this.head;
    let prev = null;
    while (current && count < index) {
      prev = current;
      current = current.next;
      count++;
    }
    if (!current && count < index) {
      return; // Return if the index exceeds the size of the list
    }
    prev.next = newNode;
    newNode.next = current;
  }

  // Delete a node at a specific index
  removeAt(index) {
    if (index < 0) {
      return;
    }
    if (index === 0) {
      this.head = this.head.next;
      return;
    }
    let count = 0;
    let current = this.head;
    let prev = null;
    while (current && count < index) {
      prev = current;
      current = current.next;
      count++;
    }
    if (!current && count < index) {
      return; // Return if the index exceeds the size of the list
    }
    prev.next = current.next;
  }
}

// Example usage of the linked list
const linkedList = new LinkedList();
linkedList.add(1);
linkedList.add(2);
linkedList.add(3);

console.log("Size of linked list:", linkedList.size()); // 3
console.log("Head of linked list:", linkedList.head()); // 1

linkedList.remove(2);
console.log("Index of 2 in linked list:", linkedList.indexOf(2)); // -1

console.log("Element at index 1:", linkedList.elementAt(1).data); // 3

linkedList.addAt(1, 4);
console.log("Size of linked list after adding at index 1:", linkedList.size()); // 3

linkedList.removeAt(0);
console.log("Head of linked list after removing at index 0:", linkedList.head()); // 4
```
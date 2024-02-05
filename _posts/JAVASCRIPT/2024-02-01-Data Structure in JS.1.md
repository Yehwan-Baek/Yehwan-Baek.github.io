---
layout: post
title: "2024-02-01-Data Structures in JS -Stack and Queue-"
categories: [Javascript]
---


# Data Structures in JS

 This post is about 2 data structures in JS that I learned. 

## Stack
Stack follows the principle of LIFO (last in, first out). If you stack books, the top book will be taken before the bottom one. When you browse on the internet, the back button leads you to the most recently browsed page.

### Methods of stack in Javascript

- **push** : Input a new element.
- **pop** : Remove the top element, return the removed element.
- **peek** : Return the top element.
- **length** : Return the number of element(s) in the stack.


### Example code
The following is a simple example code for implementing a stack in JavaScript.

```
class Stack {
  constructor() {
    this.items = [];
  }

  // Add an element to the stack
  push(element) {
    this.items.push(element);
  }

  // Remove and return an element from the stack
  pop() {
    if (this.isEmpty()) {
      return "Underflow";
    }
    return this.items.pop();
  }

  // Return the top element of the stack
  peek() {
    if (this.isEmpty()) {
      return "Stack is empty";
    }
    return this.items[this.items.length - 1];
  }

  // Check if the stack is empty
  isEmpty() {
    return this.items.length === 0;
  }

  // Return the size of the stack
  size() {
    return this.items.length;
  }
}

// Example of using the stack
const stack = new Stack();
stack.push(10);
stack.push(20);
stack.push(30);

console.log("Top of the stack:", stack.peek()); // 30
console.log("Stack size:", stack.size()); // 3

console.log("Popped element:", stack.pop()); // 30
console.log("Stack size after pop:", stack.size()); // 2
```


## Queue
Queue is similar to stack. The only difference is that queue uses the FIFO principle (first in, first out). In other words, when you queue for the bus, the first in the queue will always board first.

### Methods of queue in Javascript
- **enqueue** : Enter queue, add an element at the end.
- **dequeue** : Leave queue, remove the front element and return it.
- **front** : Get the first element.
- **isEmpty** : Determine whether the queue is empty.
- **size** : Get the number of element(s) in queue

### Example code
The following is a simple example code for implementing a stack in JavaScript.

```
class Queue {
  constructor() {
    // Array to store queue elements
    this.items = [];
  }

  // Add an element to the end of the queue (enqueue)
  enqueue(element) {
    this.items.push(element);
  }

  // Remove and return the front element from the queue (dequeue)
  dequeue() {
    // Check if the queue is empty
    if (this.isEmpty()) {
      return "Queue is empty";
    }
    return this.items.shift();
  }

  // Get the first element in the queue (front)
  front() {
    // Check if the queue is empty
    if (this.isEmpty()) {
      return "Queue is empty";
    }
    return this.items[0];
  }

  // Check if the queue is empty (isEmpty)
  isEmpty() {
    return this.items.length === 0;
  }

  // Get the number of elements in the queue (size)
  size() {
    return this.items.length;
  }
}

// Example of using the queue
const queue = new Queue();
queue.enqueue(10);
queue.enqueue(20);
queue.enqueue(30);

console.log("Front of the queue:", queue.front()); // 10
console.log("Queue size:", queue.size()); // 3

console.log("Dequeued element:", queue.dequeue()); // 10
console.log("Queue size after dequeue:", queue.size()); // 2
```
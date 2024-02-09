---
layout: post
title: "2024-02-09-Data Structures in JS -Set- "
categories: [Javascript]
---


# Data Structures in JS
 This post is about set in JS that I learned.

## Set
A set is a basic concept in mathematics: a collection of well defined and distinct objects. ES6 introduced the concept of set, which has some similarities to  an array. However, a set does not allow repeating elements and is not indexed. 

### Methods of set in Javascript
JavaScript Set does support built-in methods.
- **values**: Return all elements in a set.
- **size**: Return the number of elements.
- **has**: Determine whether an element exists.
- **add**: Insert elements into a set.
- **remove**: Delete elements from a set.
- **union**: Return the intersection of two sets.
- **difference**: Return the difference of two sets.
- **subset**: Determine whether a certain set is a subset of another set.

```
class MySet {
  constructor() {
    this.elements = [];
  }

  // values: Return all elements in a set.
  values() {
    return this.elements;
  }

  // size: Return the number of elements.
  size() {
    return this.elements.length;
  }

  // has: Determine whether an element exists.
  has(element) {
    return this.elements.includes(element);
  }

  // add: Insert elements into a set.
  add(element) {
    if (!this.has(element)) {
      this.elements.push(element);
    }
  }

  // remove: Delete elements from a set.
  remove(element) {
    if (this.has(element)) {
        const index = this.elements.indexOf(element);
        this.elements.splice(index, 1);
    }
  }

  // union: Return the intersection of two sets.
  union(otherSet) {
    const unionSet = new MySet();
    this.elements.forEach(element => unionSet.add(element));
    otherSet.values().forEach(element => unionSet.add(element));
    return unionSet;
  }

  // difference: Return the difference of two sets.
  difference(otherSet) {
    const differenceSet = new MySet();
    this.elements.forEach(element => {
      if (!otherSet.has(element)) {
        differenceSet.add(element);
      }
    });
    return differenceSet;
  }

  // subset: Determine whether a certain set is a subset of another set.
  isSubsetOf(otherSet) {
    return this.elements.every(element => otherSet.has(element));
  }
}

// Example usage of the set
const mySet = new MySet();
mySet.add(1);
mySet.add(2);
mySet.add(3);

console.log(mySet.values()); // [1, 2, 3]
console.log(mySet.size()); // 3
console.log(mySet.has(2)); // true

const anotherSet = new MySet();
anotherSet.add(3);
anotherSet.add(4);
anotherSet.add(5);

console.log(mySet.union(anotherSet).values()); // [1, 2, 3, 4, 5]
console.log(mySet.difference(anotherSet).values()); // [1, 2]
console.log(anotherSet.isSubsetOf(mySet)); // false

```
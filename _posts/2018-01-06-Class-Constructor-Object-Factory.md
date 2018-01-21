---
layout: post
title:  "Class vs Constructor vs Object vs Factory"
date:   2018-01-06 18:44:22 -08:00
tags: ['Coding','JavaScript']
---

Creating objects: Class vs Constructor vs Object literal vs Factory.

```js
// Class
class Person {
  constructor(f, l) {
    this.f = f;
    this.l = l;
  }

  speak() {
    console.log(`My name is ${this.f} ${this.l}`)
  }
}

const sonny = new Person('Sonny', 'Rollins');
sonny.speak();



// Constructor
function PersonConst(f, l) {
  this.f = f;
  this.l = l;
}

PersonConst.prototype.speak = function() {
  console.log(`My name is ${this.f} ${this.l}`);
}

const john = new PersonConst('John', 'Coltrane');
john.speak();

// Object
const personObj = {
  f: 'default',
  l: 'default',
  speak: function() {
    console.log(`My name is ${this.f} ${this.l}`);
  }
}

const joe = Object.create(personObj);
joe.f = 'Joe';
joe.l = 'Henderson';
joe.speak();

// Factory
function makePerson(f, l) {
  const p = Object.create(personObj);
  p.f = f;
  p.l = l;
  return p;
}

const wayne = makePerson('Wayne', 'Shorter');
wayne.speak();
```

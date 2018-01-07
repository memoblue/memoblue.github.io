---
layout: post
title:  "Class vs Constructor vs Object vs Factory"
date:   2018-01-06 18:44:22 -08:00
tags: ['Coding','JavaScript']
---

How to define: Class vs Constructor vs Object vs Factory.

```js
// Class
class Pig {
  speak() {
    console.log('Groink');
  }
}
const friend1 = new Pig();
friend1.speak();

// Constructor
function Cow() {}
Cow.prototype.speak = function() {
  console.log('Moooo');
};
const friend2 = new Cow();
friend2.speak();

// object
const friend = {
  speak: function() {
    console.log('blubb');
  }
};
friend.speak();

// factory
const friendship = {
  speak() {
    console.log('wazzup?');
  }
};
function makeFriend() {
  return Object.create(friendship);
}
const randomFriend = makeFriend();
randomFriend.speak();
```

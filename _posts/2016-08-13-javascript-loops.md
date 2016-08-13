---
layout: post
title:  "JavaScript Loops"
date:   2016-08-13 17:12:20 -04:00
tags: ['Coding','JavaScript']
---

Here's a run down of the most common/useful ways to loop through stuff in JavaScript.

## Arrays

### for

Probably the most common way to loop through stuff, but the syntax is verbose, ugly, and you have to access the array elements through its indexes.

```js
const colors = ['red', 'yellow', 'green'];
for(let i = 0; i < colors.length; i++) {
    console.log(colors[i]);
}
```

### for...in

The syntax is a bit better than the good old `for()` loop, but not that much. And it will loop through everything added to the prototype chain (both `stuff` and `moreStuff` show up in the console). On top of that, the iteration order is arbitrary… Not the greatest option!

```js
let colors = ['red', 'yellow', 'green'];
colors.stuff = 'Not a color'; // shows up uninvited
Array.prototype.moreStuff = 'Definitely not a color'; // this one too
for (const i in colors) {
    console.log(colors[i]);
}
```

### forEach

Arguably the cleanest way to iterate over an array and a good choice as long as you don't need to `break;` or `continue;` out of the loop.

```js
const colors = ['red', 'yellow', 'green'];
colors.forEach((color, i) => {
    console.log(`${i}: ${color}`);
});
```

### for...of

Your best option if `forEach()` doesn't fit the bill. You get the best of all worlds: It will only iterate over what it should, you don't have to use the `color[i]` type syntax, _and_ you can use `continue;` and `break;`.

```js
for (const color of colors) {
    if (color === 'yellow') {
        continue;
    }
    console.log(color);
}
```

And if you need the index for some reason, you can use the `entries()` method to get an array iterator and combine that with a little destructuring assignment syntax and you're set:

```js
for (const [i, color] of colors.entries()) {
    console.log(`${color} is #${i + 1}`);
}
```

## Objects

For objects, you're pretty much stuck with `for...in`, which means you get the same problem where stuff inherited from the prototype chain is iterated over.

```js
Object.prototype.someCoolStuff = 'Cool!'; // shows up uninvited

const me = {
    name: 'memo',
    age: 22,
    learning: ['Design', 'Code']
};

for (const key in me) {
    console.log(`${key}: `, me[key]);
}
```

The traditional way around this problem:

```js
for (const key in me) {
    if(me.hasOwnProperty(key)) {
        console.log(`${key}: `, me[key]);
    }
}
```

Another option is to take advantage of ES6 to turn the object's keys into an array:

```js
Object.keys(me).forEach((k) => {
    console.log(`${k}: `, me[k]);
});
```

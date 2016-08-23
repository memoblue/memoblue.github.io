---
layout: post
title:  "JavaScript Array Methods"
date:   2016-08-14 20:35:06 -04:00
tags: ['Coding','JavaScript']
---

For my [String methods article][str], I went for the "cheat sheet" reference approach. For arrays though, I'm going for a curated list of concrete examples highlighting the methods I've found most useful so far. That's why this list will most likely evolve a lot more over time.

Firs of, there are a couple of methods to turn stuff in arrays:

## Array.from()

`from()` turns "array-ish" stuff into real arrays. It's super useful with NodeLists, and it takes an optional map function as a callback, so if you get:

```html
<ul>
    <li>item 1</li>
    <li>item 2</li>
    <li>item 3</li>
    <li>item 4</li>
</ul>
```

You can easily get an array of all the items like that:

```js
const li = document.querySelectorAll('li'); // NodeList
const text = Array.from(li, el => el.textContent);
console.log(text); // ["item 1", "item 2", "item 3", "item 4"]
```

## Array.of()

This one is very straight forward: you feed it a bunch of arguments and you get an array back.

```js
var arr = Array.of('something', 'something else', 32, false);
console.log(arr); // ["something", "something else", 32, false]
```

## some()

Returns `true` if **some** of the values in the array return true against the callback function.

```js
const prices = [15, 23, 7, 43, 20, 43, 54, 12];
const canAffordSomething = prices.some(price => price < 20);
console.log(canAffordSomething); // true
```

## every()

Returns `true` if **every** values in the array return true against the callback function.

```js
const prices = [15, 23, 7, 43, 20, 43, 54, 12];
const canAffordEverything = prices.every(price => price < 20);
console.log(canAffordEverything); // false
```

## find() & findIndex()

Let's pretend we get this JSON data from an API:

```js
const api = [
    {
        "id": 1,
        "name": "John Coltrane",
        "albums": [
            { "title": "Giant Steps" },
            { "title": "A Love Supreme"},
            { "title": "Tenor Madness"}
        ],
        "instrument": "Saxophone"
    },
    {
        "id": 2,
        "name": "Sonny Rollins",
        "albums": [
            { "title": "Saxophone Colossus" },
            { "title": "The Bridge"},
            { "title": "Tenor Madness"}
        ],
        "instrument": "Saxophone"
    }
];
```

`find()` loops through the `api` array and returns the first element that returns true in the callback:

```js
const sonny = api.find(musician => musician.id === 2);
console.log(`Sonny plays the ${sonny.instrument}`);
```

If you need to find the index instead, just do:

```js
const sonnyPos = api.findIndex(musician => musician.id === 2);
console.log(`Sonny is #${sonnyPos + 1} in the list`);
```

## filter()

That one works the same, but it returns an array instead of just the first element.

```js
const saxPlayers = api.filter(musician => musician.instrument === 'Saxophone');
console.log(saxPlayers);
```

## map()

`map()` lets you run a function on each element of an array and create a new array with the results.

```js
const start = [2, 3, 4];
const double = start.map(el => el * 2);
console.log(double); // [4, 6, 8]
```

## reduce()

The `reduce()` method reduces an array to a single value by running a callback function that takes 4 arguments: the previous element, the current element, the current index, and (less useful) the array. It also takes an optional starting value as a second argument.

```js
[2,4,5].reduce((prev, next) => prev + next); // 11
['a','b','c'].reduce((prev, next, i) => prev + next + i, 'start: '); // 'start: a0b1c2'
```

## sort()

`sort()` sorts an existing array according to a `compare(a, b)` function which works like this:

```js
function compare(a, b) {
  if (a < b) {
    return -1; // a comes first
  }
  if (a > b) {
    return 1; // b comes first
  }
  return 0; // a = b / no order change
}
```

Here's how you'd sort an array of numbers:

```js
const arr = [25, 18, 5, 12, 2, 18];
const sorted = arr.sort((a, b) => a - b);
console.log(sorted); // [2, 5, 12, 18, 18, 25]
```

## Old School Methods

### push() pop() shift() unshift()

I'm grouping these to stick them in a table:

Methods     | Description                   | Returns
------------|-------------------------------|----------
`push()`    | add element at the end        | length
`unshift()` | add element at the beginning  | length
`pop()`     | removes last element          | element
`shift()`   | removes first element         | element

All those methods modify the original array. When they remove an element, they return it. When they add it, they return the new length of the array.

```js
const arr = ['this', 'is', 'cool'];
const arr1 = arr.push('!'); // 4
const arr2 = arr.unshift('For', 'sure'); // 6
const arr3 = arr.pop(); // !
const arr4 = arr.shift(); // For
console.log(arr); // ["sure", "this", "is", "cool"]
```

### slice()

`slice(a, b)` returns a new array "slice" starting at `a` and ending at `b` (not including `b`).

```js
const arr = [25, 18, 5, 12, 2, 18];
const slice1 = arr.slice(0, 2); // [25, 18]
const slice2 = arr.slice(2); // [5, 12, 2, 18]
const slice3 = arr.slice(-2); // [2, 18]
const slice4 = arr.slice(1, -2); // [18, 5, 12]
console.log(arr); // [25, 18, 5, 12, 2, 18];
```

### join()

`join()` joins all elements of an array into a string, with an (optional) separator.

```js
const arr = ['this', 'is', 'cool'];
const str = arr.join(' ');
console.log(str); // "this is cool"
```

### concat()

This function is much less useful than it used to be since the introduction of the spread operator in ES6, but here's how it works:

```js
const first = [1, 2];
const second = [3, 4];
const third = [5, 6];
const whole = first.concat(second, third);
console.log('whole:', whole); // [1, 2, 3, 4, 5, 6]
```



[str]:{% post_url 2016-06-03-javascript-string-methods %}

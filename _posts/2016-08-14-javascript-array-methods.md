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

## Array.some()

Returns `true` if **some** of the values in the array return true against the callback function.

```js
const prices = [15, 23, 7, 43, 20, 43, 54, 12];
const canAffordSomething = prices.some(price => price < 20);
console.log(canAffordSomething); // true
```

## Array.every()

Returns `true` if **every** values in the array return true against the callback function.

```js
const prices = [15, 23, 7, 43, 20, 43, 54, 12];
const canAffordEverything = prices.every(price => price < 20);
console.log(canAffordEverything); // false
```

## Array.find() & Array.findIndex()

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

## Array.filter()

That one works the same, but it returns an array instead of just the first element.

```js
const saxPlayers = api.filter(musician => musician.instrument === 'Saxophone');
console.log(saxPlayers);
```

## Array.map()

`map()` lets you run a function on each element of an array and create a new array with the results.

```js
const start = [2, 3, 4];
const double = start.map(el => el * 2);
console.log(double); // [4, 6, 8]
```

## Array.reduce()

The `reduce()` method reduces an array to a single value by running a callback function that takes 4 arguments: the previous element, the current element, the current index, and (less useful) the array. It also takes an optional starting value as a second argument.

```js
[2,4,5].reduce((prev, next) => prev + next); // 11
['a','b','c'].reduce((prev, next, i) => prev + next + i, 'start: '); // 'start: a0b1c2'
```

[str]:{% post_url 2016-06-03-javascript-string-methods %}

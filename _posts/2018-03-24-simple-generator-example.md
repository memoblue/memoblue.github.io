---
layout: post
title:  "SIMPLE Generator example"
date:   2018-03-24 11:22:49 -07:00
tags: ['Coding','JavaScript']
---

Yes, you should use async/await to query an API. But every generator function tutorial I found online was waaaay too complicated for me, and I found messing around with an API the best way to understand how they work.

This assumes you already read the [MDN docs][mdn] but you're still confused and those [crazy][tut1] [tutorials][tut2] didn't really help.

I picked the [Ghibli API][api] because… Who doesn't like Totoro?

For my test, I figured I'd hit the `/species` endpoint to get the id of the "Cat" species (which is actually the `url` property). Then pass that id (`url`) to filter the `/people` endpoint to get a list of all the cats. Finally, just add that as a list in the DOM.

It feels like the bear minimum but still realistic example.

### Get the id for the "Cat" species

First you get all the species, and then find the one object in the array that has a name of `Cat` and get its `url` property:

```js
function getCatId() {
  fetch('https://ghibliapi.herokuapp.com/species')
    .then(data => data.json())
    .then((data) => {
      const catId = data.find(s => s.name === 'Cat').url;
    });
}
```

### Filter the people with this id

Then you filter the people array so that you only get the object with a `spicies` property equal to the id (`url`) you got previously.

```js
function getCats(catId) {
  fetch('https://ghibliapi.herokuapp.com/people')
    .then(data => data.json())
    .then((data) => {
      const cats = data.filter(c => c.species === catId);
    });
}
```

Of course, the problem is to make sure the first fetch is done before you call the second, otherwise your `catId` might be equal to nothing. And that's where generator functions come in handy.

You basically do something like this:

```js
function* listCats() {
  const id = yield getCatId();
  const list = yield getCats(id);
}

const gen = listCats();
gen.next();
```

Two things that confused the hell out of me:

**First:** when you call the `listCats()`, nothing happens. That's because you're really just generating an special object on wich you can call `.next()` to go through the different `yield` you setup. And that's about it.

**Second:** that `const id = yield getCatId();` syntax really looks like you're sticking the returned value of `getCatId()` in `id`, but that's totally NOT what you're doing. Nope. What you're really doing is sticking whatever is in `.next(stuffGoingIntoId)` in `id`. So you gotta make sure you call that `.next()` in your `getCatId()` and you pass it what you need.

So if we revisit our functions from earlier, and add those `.next()` calls, the whole thing looks like that:

```js
/* eslint-disable no-use-before-define */

// get the ID for "Cat" species in the Ghibli API
function getCatId() {
  fetch('https://ghibliapi.herokuapp.com/species')
    .then(data => data.json())
    .then((data) => {
      const catId = data.find(s => s.name === 'Cat').url;
      gen.next(catId);
    });
}

// Get all the cats from the people endpoint
function getCats(catId) {
  fetch('https://ghibliapi.herokuapp.com/people')
    .then(data => data.json())
    .then((data) => { 
      const cats = data.filter(c => c.species === catId);
      gen.next(cats);
    });
}

// Add the cat names to a UL in the DOM
function listNames(cats) {
  const listItems = cats.map(item => `<li>${item.name}</li>`).join('');
  const list = document.createElement('ul');
  list.innerHTML = listItems;
  document.body.appendChild(list);
}

function* listCats() {
  const id = yield getCatId();
  const list = yield getCats(id);
  listNames(list);
}

const gen = listCats(); // setup the generator object
gen.next(); // get the ball rolling
```

[mdn]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function*
[api]:https://ghibliapi.herokuapp.com/
[tut1]:https://davidwalsh.name/es6-generators
[tut2]:https://medium.com/@dtothefp/why-can-t-anyone-write-a-simple-es6-generators-tutorial-ec2bbdf6ff45

---
layout: post
title:  "How to make calls in parallel with async/await"
date:   2018-04-24 09:25:27 -07:00
tags: ['Coding','JavaScript']
---

In my [generator example][gen], I mentionned you should really do that with async/await, so here's how you'd do it.

I'm using the [Ghibli API][api] for my examples because… Totoro!

It's much shorter and easier to read than the [generator function version][gen], so… Definitely the way to go. But it good to know how generators work too.

```js
// Add the cat names to a UL in the DOM
function listNames(cats) {
  const listItems = cats.map(item => `<li>${item.name}</li>`).join('');
  const list = document.createElement('ul');
  list.innerHTML = listItems;
  document.body.appendChild(list);
}

async function listCats() {
  const [species, people] = await Promise.all([
    fetch('https://ghibliapi.herokuapp.com/species').then(data => data.json()),
    fetch('https://ghibliapi.herokuapp.com/people').then(data => data.json()),
  ]);
  const id = species.find(s => s.name === 'Cat').url;
  const cats = people.filter(c => c.species === id);
  listNames(cats);
}

listCats();
```

[gen]:{% post_url 2018-03-24-simple-generator-example %}
[api]:https://ghibliapi.herokuapp.com/

---
layout: post
title:  "Use filter() as a Conditional"
date:   2017-03-19 09:02:00 -04:00
tags: ['Coding','JavaScript','tip','one liner']
---

Quick tip on how to conditionally concatenate something at the end of a string depending on wether the API returns it or not, with a slick one liner:

```js
const player1 = {
    name: 'Sonny Rollins',
    inst: 'Saxophone'
}
const player2 = {
    name: 'John Coltrane'
}
const sonny = [player1.name, player1.inst].filter(att => !!att).join(' - '); // Sonny Rollins - Saxophone
const john = [player2.name, player2.inst].filter(att => !!att).join(' - '); // John Coltrane
```

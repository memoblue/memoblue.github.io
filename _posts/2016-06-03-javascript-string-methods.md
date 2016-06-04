---
layout: post
title:  "JavaScript string methods"
date:   2016-06-03 18:09:13 -04:00
tags: ['Coding','JavaScript']
---

There are 49 string methods [listed on MDN][0]… So I thought I'd go through all of them and try to figure out which ones I should know well. That's what I narrowed it down to.

## The good stuff

Methods                 | Description                               | Specs | Docs
------------------------|-------------------------------------------|-------|---------
`str.charAt(pos)`       | character at `pos`                        |       | [MDN][1]
`str.endsWith(a)`       | `str` ends with `a` ?                     | ES6   | [MDN][2]
`str.includes(a)`       | `a` is in `str`? (case sensitive)         | ES6   | [MDN][3]
`str.indexOf(a)`        | position of first `a`                     |       | [MDN][4]
`str.lastIndexOf(a)`    | position of last `a` from end             |       | [MDN][5]
`str.match(/a/g);`      | array off all "a" (only 1st if not `g`)  |       | [MDN][6]
`str.repeat(n)`         | string of `str` * `n`                      | ES6   | [MDN][7]
`str.replace(a, b)`     | replace `a` (regex/str) with `b` (str/fn) |       | [MDN][8]
`str.search(regexp)`    | position of first `regexp`                |       | [MDN][9]
`str.slice(start, end)` | string from `start` to `end`              |       | [MDN][10]
`str.split(',')`        | array of `str` elements separated by `,`  |       | [MDN][11]
`str.startsWith(a)`     | `str` starts with `a` ?                   | ES6   | [MDN][12]
`str.substr(start, l)`  | string from `start` of length `l`         |       | [MDN][13]
`str.toLowerCase()`     | `str` to lower case                       |       | [MDN][14]
`str.toUpperCase()`     | `str` to upper case                       |       | [MDN][15]
`str.trim()`            | removes whitespace from `str`             |       | [MDN][16]

I'm going to ignore the deprecated and experimental methods, and quickly go over the more esoteric ones below.

## The rest

### Unicode

The Unicode related methods are useful when you need them, but I'm fine with looking them up when that happens.

```
String.fromCharCode()  // old, faster, doesn't cover all Unicode values
str.charCodeAt(index)  // old, etc.
String.fromCodePoint() // ES6, slower, works with ALL legal Unicode values
str.codePointAt(pos)   // ES6, etc.
str.normalize()
```

### Spotty browser support

```
str.localeCompare() // string sorting with i18n features
```

### Not super useful

```
str.anchor() // I can't think of why I'd want to use this
str.concat() // just use +
str.link() // make an <a> HTML element… woohoo…
str.substring() // just use slice()
str.toString() // not sure why I'd want to use it on a string…
str.valueOf() // "This method is usually called internally by JavaScript"
```

[0]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String
[1]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charAt
[2]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith
[3]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes
[4]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf
[5]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf
[6]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match
[7]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/repeat
[8]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace
[9]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/search
[10]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice
[11]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split
[12]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith
[13]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substr
[14]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLocaleLowerCase
[15]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase
[16]:https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/Trim

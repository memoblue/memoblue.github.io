---
layout: post
title:  "CSS Selectors"
date:   2016-07-04 17:08:14 -04:00
tags: ['Coding','CSS']
---

This is not an exhaustive run down of all the CSS selectors known to mankind. It's more of a curated list of CSS selectors that are traditionally underutilized, yet extremely useful.

**Adjacent sibling selector** [→][1] Match `b` if `a` and `b` are siblings and if `b` is right after `a`.

```css
a + b {}
```

---

**General sibling selector** [→][2] Match any `b` if `a` and `b` are siblings and `b` is after `a`.

```css
a ~ b {}
```

---

**Direct descendant selector** [→][3] Match `b` if it's a (direct) child of `a`.

```css
a > b {}
```

---

**Attribute selector** [→][4] Match any `a` that has a `b` attribute.

```css
a[b] {}
```

With attribute selectors, you can use a regex inspired syntax to target elements based on the value of their attributes:

```scss
a[b="c"] {}  // `a` that has a `b` equal to `c`
a[b*="c"] {} // `a` has `c` somewhere in `b`
a[b^="c"] {} // `a` has a `b` that starts with `c`
a[b$="c"] {} // `a` has a `b` that ends with `c`
a[b~="c"] {} // `a` has `c` somewhere in `b` and `b` is a space separated list
a[b|="c"] {} // `a` has `c` somewhere in `b` and `b` is a dash separated list
```

**Tip:** if you'd like to use CSS class names that require escaping in CSS but don't want the ugly syntax that goes with it, you can use attribute selectors to target your classes instead:

```css
[class="1/4"] {}
```

**Note:** all those are case sensitive and although there's a new `i` flag to make them case insensitive, as of this writing the browser support is pretty spotty.

---

There are also a [bunch of pseudo-classes][mdn] available… The most useful by far are those three:

**:not()** [→][5] Matches any `a` that does not have `b` (it does **not** add to the selector specificity, unlike other pseudo-classes, the specificity is defined by its argument).

```scss
a:not(b) {}

div:not(.some-class) {} // no quotes for class/id names
```

**:nth-of-type()** [→][6] Match any `e` who are children of the same parent and whose numeric positions match `an+b` (`an` is the "frequency" and `b` the "offset") within the collection of elements of type `e`.

```css
e:nth-of-type(an + b) {}
```

**:nth-child()** [→][7] Match any `e` who are children of the same parent and whose numeric positions match `an+b` (`an` is the "frequency" and `b` the "offset") within the collection of all siblings.

```css
e:nth-child(an + b) {}
```

Here's a [quick example][8] of the difference between`:nth-child` and `:nth-of-type`. And here's a [great resource][9] if you want to play with them visually.

[1]:http://codepen.io/memoblue/pen/ZOyXNX
[2]:http://codepen.io/memoblue/pen/grGBro
[3]:http://codepen.io/memoblue/pen/qNPJBb

[4]:http://codepen.io/memoblue/pen/QEqkGz

[5]:http://codepen.io/memoblue/pen/ZOvkBJ
[6]:http://codepen.io/memoblue/pen/XKVQak
[7]:http://codepen.io/memoblue/pen/PzEgBP
[8]:http://codepen.io/memoblue/pen/ZOvkZX

[9]:https://css-tricks.com/examples/nth-child-tester/
[mdn]:https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes

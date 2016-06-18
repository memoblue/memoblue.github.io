---
layout: post
title:  "React lifecycle methods"
date:   2016-06-17 23:53:46 -04:00
tags: ['Coding','Cheat Sheet','JavaScript','React']
---

The [React component specs][1] are a bit cryptic, but the basic idea is that `render()` shouldn't modify the component's `state` or interact with the DOM directly. For that, you got lifecycle methods at your disposition.

## Lifecycle overview

![React component lifecycle](/assets/react-component-lifecycle.png)

## Lifecycle methods

### Mounting

Name     | called       | use setState()
---------|--------------|--------------------
`componentWillMount()` | before `render()` | ok
`componentDidMount()` | after `render()` | ok? ([maybe not][1])

### Updating

Name     | called       | use setState()
---------|--------------|--------------------
`componentWillReceiveProps()` | new `props` | ok
`shouldComponentUpdate()` | new `props`/`state` | no
`componentWillUpdate()` | new `props`/`state` | no
`componentDidUpdate()` | new `props`/`state` | ok

### Unmounting

Name     | called       | 1st render() | use setState()
---------|--------------|--------------------
`componentWillUnmount()` | before unmounting | not called | no

## Examples

Here are a few common scenarios for when you'd want to use these methods:

**componentDidMount**

* Ajax to fetch data from an API, etc.
* Set up listeners (Firebase, etc.)
* Set timers using `setTimeout` or `setInterval`

**componentWillReceiveProps**

* Update `state` in response to a `prop` change

**componentDidUpdate**

* Check on `state` values set via a timer, etc.
* Operate on the DOM when the component has been updated

**componentWillUnmount()**

* Remove any listeners you initially set up
* Clear timers

[1]:https://facebook.github.io/react/docs/component-specs.html
[2]:https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-did-mount-set-state.md

---
layout: post
title:  "ESLint Setup in Atom"
date:   2016-08-17 08:58:58 -04:00
tags: ['Coding','JavaScript']
---

If you don't have them installed already, make your life easier and install [Homebrew][1] first, then use it to install [nodenv][2]. Once that's done. Make sure you install a recent version of node and npm via `nodenv`.

## Install

There are 2 ways to install ESLint, globally: `npm install -g eslint` or within a project, using `npm install` with a `package.json` file. Both a global and project specific setup can coexist since ESLint will look for the `.eslintrc` file that is the closest to your current directory on your system.

Personally, I prefer to setup ESLint per project. It's more portable and flexible that way.

There are a few steps needed to get ESLint to work in Atom:

1. Install ESLint in your project
2. Setup your `.eslintrc` file
3. Install the [Linter package][3]
4. Install the [linter-eslint package][4]
5. Setup a few prefs in Atom

## Install ESLint

ESLint won't do anything until you specify which presets you want to use. A popular option nowadays is [eslint-config-airbnb][5]. You can use the install instructions there or just copy these to your project's `package.json` file and run `npm install`:

```json
"devDependencies": {
  "eslint": "^3.3.1",
  "eslint-config-airbnb": "^10.0.1",
  "eslint-plugin-html": "^1.5.2",
  "eslint-plugin-import": "^1.13.0",
  "eslint-plugin-jsx-a11y": "^2.1.0",
  "eslint-plugin-react": "^6.1.2"
}
```

## Setup your `.eslintrc` file

I stick mine at the root of the projects I'm working on, and it looks like that:

```json
{
  "env": {
    "node": true,
    "browser": true,
    "es6": true
  },
  "extends": "airbnb",
  "rules": {
    "comma-dangle": 0,
    "no-console": 0,
    "no-unused-vars": 1
  },
  "plugins": [
    "html"
  ]
}
```

Basically, what that says is: "let me write Node, browser, and ES6 specific JavaScript using the airbnb presets, but don't give me errors if I don't put an extra comma at the end of my objects, don't freak out if I use `console.log()`, and give me a warning instead of an error when I have variables I'm not using (yet!) in the file" (the HTML plugin is to be able to write JavaScript inside `<script>` tags).

## Atom Setup

The next 2 steps are self explanatory. Just install the 2 packages listed above.

For the Atom settings, I'd recommend turning off "Show Inline Error Tooltips" in the linter package settings, and you'll also need to tell Atom which version of ESLint to use if you're using it globally. That's under "Global Node Installation Path" in the linter-eslint package settings. With nodenv, it will look like: `/Users/your-account/.nodenv/versions/x.x.x`

And that's about it! You might have to restart Atom to get ESLint to work as expected. Once it's all setup, it almost feels like magic. You'll wonder how you survived without it until now.

[1]:http://brew.sh
[2]:https://github.com/nodenv/nodenv#homebrew-on-mac-os-x
[3]:https://atom.io/packages/linter
[4]:https://atom.io/packages/linter-eslint
[5]:https://www.npmjs.com/package/eslint-config-airbnb

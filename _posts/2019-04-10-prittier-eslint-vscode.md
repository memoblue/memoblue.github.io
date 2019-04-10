---
layout: post
title: "VS Code setup with Eslint and Prittier"
date: 2019-04-10 08:37:56 -07:00
tags: ["Coding", "JavaScript", "vscode", "Workflow"]
---

Quick overview on how to setup [Prettier][1] and use it with [ESLint][2] in VS Code. That way Prittier will use your ESLint setup to format your code on save, and use its own defaults for what is not specified in your ESLint setup.

## Install ESLint

Don't bother installing it globally if you want Prettier to work with it. [Airbnb defaults][3] are a good place to start:

```
npx install-peerdeps --dev eslint-config-airbnb
```

Your `package.json` file should look something like that (I also added the `html` one manually in this example):

```json
{
  [...]
  "devDependencies": {
    "eslint": "^5.3.0",
    "eslint-config-airbnb": "^17.1.0",
    "eslint-plugin-import": "^2.16.0",
    "eslint-plugin-jsx-a11y": "^6.2.1",
    "eslint-plugin-react": "^7.12.4",
    "eslint-plugin-html": "^5.0.3"
  }
}
```

I got [more detailed info][4] on that in an old post if you need.

## Install VS code extensions

-   [ESLint](https://marketplace.visualstudio.com/itemdetails?itemName=dbaeumer.vscode-eslint)
-   [Prettier - Code formatter](https://marketplace.visualstudio.com/itemdetails?itemName=esbenp.prettier-vscode)

## Setup .eslintrc file

Here's a simplified version of what it should look like:

```json
{
    "env": {
        "node": true,
        "browser": true,
        "es6": true
    },
    "extends": "airbnb",
    "rules": {
        "comma-dangle": 1,
        "no-console": 0,
        "no-unused-vars": 1
    },
    "plugins": ["html"]
}
```

## Setup VS code extensions

The simplest way to go about this is to spend 5 minutes to go through all the options in the prefs, but the one thing you need to set to "on" is:

```json
"prettier.eslintIntegration": true
```

I also like to set the "format on save" feature to `true`, VS Code will ask you which formatter to use the first time if you got more than one install, super easy "set it and forget it" which make life much easier!

```json
"editor.formatOnSave": true
```

[1]: https://eslint.org
[2]: https://prettier.io
[3]: https://www.npmjs.com/package/eslint-config-airbnb

[4]:{% post_url 2016-08-17-eslint-setup-atom %}

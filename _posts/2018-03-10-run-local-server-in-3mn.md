---
layout: post
title:  "How to run a local server for development in 3 mn or less"
date:   2018-03-10 09:58:36 -08:00
tags: ['Coding','Tip']
---

**Step 1:** Install [Browsersync](https://browsersync.io):

`npm install -g browser-sync`

**Step 2:** Go to the folder you want to run a local server from:

`cd where/you/want/to/run/server/from`

**Step 3:** Start Browsersync:

`browser-sync start --server --files --directory "*.js, *.html, *.css"`

That's it!

You can do a lot more with Browsersync. Check out the different options in their [docs](https://browsersync.io/docs/command-line).

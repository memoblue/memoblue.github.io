---
layout: post
title:  "Fixing npm Permission"
date:   2016-11-06 18:37:11 -05:00
tags: ['Coding','JavaScript','npm','Workflow']
---

On OS X, it's pretty common to run into an `EACCES` error while trying to install npm packages. The easiest way to deal with this is to use [nodenv][1] (and the easiest way to install `nodenv` is with [Homebrew][2]). But, if for some reason you need to deal with the default `npm` directory, you'll have to change its permission to be able to install packages globally (without using `sudo`).

1. Find where npm is installed: `npm config get prefix`
2. You'll probably get something like `/usr/local`
3. Then all you got to do is run `sudo chown -R user_name /usr/local/`

If you don't know what your `user_name` is, you can run `whoami` to get it.

To make sure the new permissions have been applied to everything, you can run `ls -la` on that directory (`ls` to list files, `-l` to show the permissions and `-a` to show invisible files too).

That should do it!

[1]:https://github.com/nodenv/nodenv
[2]:http://brew.sh

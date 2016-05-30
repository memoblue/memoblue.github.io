---
layout: post
title:  "GitHub Pages gem for Jekyll"
date:   2016-05-29 22:32:11 -04:00
tags: ['Coding','GitHub','Ruby','Jekyll']
---

The [Jekyll docs][1] say that if you host your site on GitHub, you should use the `github-pages` gem to manage Jekyll's dependencies so when you deploy your site to GitHub, your local gem versions will be in sync with the ones currently on GitHub Pages.

But when I installed that gem, it totally broke my Jekyll install. It wouldn't build anymore. Instead, I got a not so helpful error: "Dependency Error: Yikes! It looks like you don't have kramdown or one of its dependencies installed. In order to use Jekyll…"

After a bunch of Googling, I came to the conclusion that if I installed [rbenv][2] instead of using the system's ruby version, the problem would most likely go away.

I already had [Homebrew][3] on my Mac, so I used it to install `rbenv`, just following the instructions in the readme. The only part that tripped me up for a bit was my `~/.bash_profile` setup, but once I added this stuff, everything else fell into place and Jekyll was fixed:

```
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"
```


[1]:https://jekyllrb.com/docs/github-pages/#deploying-jekyll-to-github-pages
[2]:https://github.com/rbenv/rbenv
[3]:http://brew.sh

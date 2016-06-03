---
layout: post
title:  "How to fix Atom's markdown-preview shortcut"
date:   2016-06-03 09:36:59 -04:00
tags: ['Tip','Blogging','Atom']
---

The [markdown-preview][1] Atom plugin is perfect for blogging. But for some reason, I never got the "Toggle Preview" shortcut to work… Until today!

**Long story short:** [Emmet][2], another fantastic plugin, was taking over that shortcut. So I had to tell Atom to override that for me.

**Long story long:** when you hit `⌘.` in Atom, it will open the `Key Binding Resolver` window at the bottom. Then you can hit the "Toggle Preview" shortcut and you'll get some very useful info:

```
emmet:merge-lines    atom-text-editor:not([mini])    /Users/memo/.atom/.../keymap.cson
```

Once you know who the culprit is, it's pretty straight forward:
* Go to "Atom > Preferences > Settings > Keybindings" and copy that command
* Click on the "your keymap file" link on that page and paste it there
* Replace the command with what you want to be triggered
* Save… Done!

In my case (overriding emmet with markdown-preview) looks like that:

```
'atom-text-editor:not([mini])':
  'ctrl-shift-M': 'markdown-preview:toggle'
```

[1]:https://github.com/atom/markdown-preview
[2]:http://emmet.io

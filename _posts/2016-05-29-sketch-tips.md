---
layout: post
title:  "Sketch tips"
date:   2016-05-29 15:05:04 -04:00
tags: ['Design','Tip','Sketch']
---

These are the highlights of what I learned reading the official [Sketch documentation][1] and a couple blog posts here and there.

The [official shortcuts list][5] is a great source of info.

## Paths

1. Hold down the `⌘` key while moving a **vector point** to make Sketch ignore "smart guides".
1. `Layer > Round to Pixel` is useful for pixel perfect designs but it won't be respected when resizing groups, and the group itself might have different `x` and `y` coordinates than the layers it contains after resize.
1. Use `Layer > Path > Rotate Copies` to create copies of a shape around a circular path.
1. When using input fields in the inspector to change values, use the return key one more time to shift the app's focus back to canvas (so for instance, you can use the R key to make a rectangle instead of typing "r" in the field).
1. You can add R/L/T/B/C/M after the value in the inspector's "Size" section to resize from right, left, top, bottom, center, middle.
1. You can specify the radius or a rectangle individually using the TL/TR/BR/BL format.
1. You can use percentages and maths to set size of layers.
1. `⌘` + click on a line between two points to insert the point exactly in the middle of the line.
1. `⌘` + click corner to rotate a layer on the fly.
1. In rotate mode: reposition the rotation axis by click + dragging it.
1. In transform mode: use `⌘` if you don't want edit a single point at a time instead of the default "3D mirror" effect.
1. To make an arc, set the border of an oval to have a huge "gap" (like 1000+) and then adjust the "dash" value visually.

## Layers

1. `⌘` + click to select nested layer in a group.
1. `⌥` + click to select second layer below overlapping layers.
1. `⌥⌘` + click and drag anywhere to move currently selected layer (without changing the current selection, independently from where you click).
1. When you click and drag to select layers, hold down `⌥` to only select layers that lie entirely within the bounds of the selection rectangle.
1. To align to a specific layer, lock that layer and select everything (from layer palette).
1. `⌥` + click on aligning buttons to align layers to artboard.
1. `⌘` + `→` to resize selected layer.
1. To resize a layer **and its properties**, use `Edit > Scale` (`⌘` + `k`).
1. Drag anything from the layer panel onto the artboard to instantly create a bitmap copy at scale (a quick way to export/import a smaller version of an image in one drag and drop).
1. Use `Edit > Set Style as Default` to setup your default shapes etc.
1. `⌥⌘` + `c` to copy style of selected layer;`⌥⌘` + `v` to paste it.
1. You can use `make grid` to duplicate art boards, but [Craft][2] is the best option to duplicate layers.

## Colors

1. Drag swatch out of the color palette to delete it (with OS X style "puff cloud" effect).
1. `⌃` + `c` to get color picker.
1. Use `1`-`9` key when a gradient stop is selected to position it 10%-90%.

## Plugins

1. Use [Sketch Toolbox][3] to manage your plugins.
1. [Craft][2] is by far the best and a "must have" plugin for Sketch.
1. [Wanderer][3] allows you to finally navigate you layer list without frustration
1. [Artboard Tools][4] is not as impressive, but I use it more than Craft.
1. [SVGO Compressor] is a port of SVGO right into Sketch!

[1]:https://www.sketchapp.com/learn/documentation/
[2]:https://labs.invisionapp.com/craft
[3]:https://github.com/turbobabr/sketch-wanderer
[4]:https://github.com/frankko/Artboard-Tools
[5]:https://www.sketchapp.com/learn/documentation/13-other/3-shortcuts.html
[6]:https://github.com/BohemianCoding/svgo-compressor

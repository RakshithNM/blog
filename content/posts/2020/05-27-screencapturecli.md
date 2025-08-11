---
title: Screencapture using CLI
date: 2020-05-27
published: true
tags: ['CLI', 'ScreenCapture', 'MacOS']
cover_image: ./images/screencapture.png
canonical_url: false
description: "Guide to using CLI to capture screenshots interactively"
---

I wanted a screenshot of a tooltip on a website that i was working on. It isnt possible to do this using the GUI tools as it is not possible to capture the hover state in the screencapture.

```screencapture -T 5 -C -i ~/Desktop/screencapture.jpg```

Go to the terminal, copy paste the instruction above. Now you can interactively select the region you want to be capture.

After the duration(5 in the example above) the selected region is now in the location specified(~/Desktop/screencapture.jpg).

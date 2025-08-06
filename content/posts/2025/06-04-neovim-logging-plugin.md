---
title: Neovim logging plugin
date: 2025-04-06
published: true
tags: ['Neovim','Typescript', 'Javascript', 'Debugging']
description: "Neovim plugin to debug typescript and javascript files using log
statements"
---

People debug typescript and javascript(even NodeJs) files using log statements
more than they like to admit. I built a neovim plugin to do just that.

The most basic thing that the plugin does is it puts the word under cursor in a
`console` statement. It provides few mappings to manage debugging using log
statements.

# Features
* Insert a console log above or below the current line
* Remove all console logs in the buffer (including commented ones)
* Comment out every console log in the buffer
* Toggle the verbosity level(log, warn, info, error) used when inserting logs
* Optionally restrict mappings to specific filetypes

# Installation
Supported by all package managers

# Usage
```
<leader>wla  log word below cursor
<leader>wlb  log word above cursor
<leader>dl   remove all console logs
<leader>kl   comment out console logs
<leader>tll  toggle log level
```

[Link to the repo](https://github.com/RakshithNM/logdebug.nvim).

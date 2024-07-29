---
title: My development workflow
date: 2022-07-23
published: true
tags: ['workflow', 'editor', 'git']
canonical_url: false
description: "Rundown of my developement workflow, how i launch my development environment, edit code and commit it"
---

This blog post is a rundown of my development workflow. The tools, customisations and integrations I have setup to arrive at a workflow that helps me daily in going about my work.

# TOOLS and INTEGRATIONS within them that power my setup

* [WARP.DEV](https://www.warp.dev/) - Teminal
* [tmux](https://github.com/tmux/tmux/wiki) - Terminal multiplexer
* [tmuxinator](https://github.com/tmuxinator/tmuxinator)
* [vim](https://www.vim.org/) - Editor
>  * [fzf](https://github.com/junegunn/fzf) - Fuzzy finder
>  * [Ripgrep](https://github.com/BurntSushi/ripgrep) - Grep
>  * [Lazygit](https://github.com/jesseduffield/lazygit) - TUI for git
>  * [LogDebug](https://github.com/RakshithNM/logdebug.vim) - Debugging helper vim plugin

We might have to run several commands get our project running, make changes and commit code. For example

* Run the frontend server
* Run the backend server
* The build command
* The SSL proxy
* The database server
* Git commands - if we use the terminal

# The brute force approach is to open N terminals windows for N commands. But jumping between those windows is going to be messy as we go about doing our job.

- I personal use panes in tmux to run multiple commands. Switching between panes is much better than switching between windows.
- If we accidentally close a window(which is easy to do when we are juggling between windows of the same application) and don't use tmux there is no way to get back the session.
- Easily launch projects and run the commands that setup the project and launch editor - using tmuxinator

# Having to run many commands to get our project running each time is highly inefficient.

- I create a tmuxinator project, set it up and then add a alias in `~/.zshrc` like `alias project=tmuxinator start project` [project ideally should be the name of the project :)]
- All the different panes and the commands to run in those panes will be set up in the `~/.tmuxinator/project.yml` [project ideally should be the name of the project :)]
- With this setup starting any project is just running the project with its name `project`

# Editor workflow

- I use vim not VSCode(we should use [VSCodium](https://vscodium.com/) instead) atm.
- Programming majorly involves editing code rather than adding code, so it becomes extremely crucial to be able to switch between files and grep the code as efficiently and quickly as possible.
- I use fzf to open popup within vim to search for files. The fzf popup is triggered by `<Ctrl-p>` vim key-binding. Once we have the search highlighted in the popup, pressing enter takes us to the file.
- To grep the codebase, ripgrep is my tool. Similar to fzf, ripgrep can be triggered by `<Ctrl-f>` vim key-binding.

Literal code editing workflow optimizations are left out of this blog as that will need to be a separate post.

# Git

- Using a separate terminal window for git is fine, but I wanted to avoid that(less windows the better).
- I use lazygit for git and once I got to know about it there was no looking back, and there has to be a way to use it from within vim :wink:
- Lazygit needs a terminal and we can launch terminal within vim, but I did not want to open a pane/tab/split to do that.
- Enter [floaterm](https://github.com/voldikss/vim-floaterm) - terminal in a popup. We can open a terminal in a popup and run lazygit all in once mapping `nnoremap <silent> lg :FloatermNew --height=1.0 --width=0.99 --name=lazygit lazygit<CR>`. As we might have figured by now, launching it from vim is just pressing `lg` in normal mode.
- After doing the git operations in the lazygit popup, quitting the lazygit popup is just pressing `q`
- Lazygit is pretty cool, after pushing the code on branch we can create a PR by pressing `o`(launches a browser tab with the PR creation screen).

# Debugging

- Log debugging is the frequent thing I do, even if i don't like to admit as much.
- I buit a vim plugin to make myself more efficient log debugging javascript and typescript files.
- Learn more on the my github [here](https://github.com/RakshithNM/logdebug.vim).

> My development workflow is optimized for working on a project for a long term. There is a little overhead with setting these tools up, but once we get into the rabbit hole of customising our development workflow, it is going to bring joy. It also makes us more efficient as the days pass.



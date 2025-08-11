---
title: Direcory wide search using quickfix list in Neovim
date: 2025-08-11
published: true
tags: ['Vim', 'Neovim', 'Workflow', 'Search']
description: "Quick way to search for all references of a word under cursor"
---

If i am reading code and want to see all references of a word, until yesterday i
have been opening the grepping popup to type the word that i am interested in
searching for and then using the popup to preview the file contents.

I have a new workflow now. I have updated my configuration to search for the
word under cursor and populate the quickfix list with all the references of the
word. I have keymaps that make this a breeze.

```lua
-- <leader>gr => grep word under cursor, open quickfix
vim.keymap.set('n', '<leader>gr', function()
  local word = vim.fn.expand('<cword>')
  if word == nil or word == '' then return end
  vim.cmd('silent! grep! ' .. vim.fn.shellescape(word))
  vim.cmd('copen')
end, { desc = 'Grep <cword> and open quickfix' })

map('n', '<leader>q', ':cclose<CR>', { silent = true, desc = 'Quickfix: close' })
map('n', '<leader>cn',':cnext<CR>', { silent = true, desc = 'Quickfix: next' })
map('n', '<leader>cp',':cprevious<CR>', { silent = true, desc = 'Quickfix: prev' })
```

* BONUS TIP

Since it uses the quickfix list you can replace all the references of `<cword>` in the directory by using the substitue
command `:cdo s/[find]/[replace]/gc`

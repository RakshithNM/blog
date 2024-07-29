---
title: Presentations in vim
date: 2021-01-02
published: true
tags: ['presentation','vim', 'markdown']
cover_image: ./images/vim-presentation.png
canonical_url: false
description: "Use vim as a presentation tool"
---

Vim can be used to give presentations. You need few plugins to do it.

1. [vim-pandoc](https://github.com/vim-pandoc/vim-pandoc) - vim pandoc doesnt come with syntax highlighting so you need to install [vim-pandoc-syntax](https://github.com/vim-pandoc/vim-pandoc-syntax)

2. You can create your own file extension for the slides, i have a file extension called `.rvpm`
3. [Goyo](https://github.com/junegunn/goyo.vim) - this is to remove all the vim items like the line number.
4. Add the following lines to your `vimrc`
```js " For table mode
nnoremap <silent> <leader>tm :TableModeToggle<CR>

' treat rvpm files as pandoc
augroup filetype_md
  autocmd!
  autocmd bufread,bufnew *.rvpm set filetype=pandoc
augroup end

' Open rvmp files as presentation
autocmd BufNewFile,BufRead *.rvpm call SetRakshithsVimPresentaionMode()
function SetRakshithsVimPresentaionMode()
  nnoremap <buffer> <Right> :n<CR>
  nnoremap <buffer> <Left> :N<CR>

  if !exists('#goyo')
    Goyo
  endif
endfunction

let g:pandoc#syntax#codeblocks#embeds#langs = ["javascript", "go", "bash=sh"]

' Hide ~ on empty lines
hi! EndOfBuffer ctermbg=bg ctermfg=bg guibg=bg guifg=bg
```
5. Create a directory for your presentation.
6. `cd` into the directory and open all files using `vim *`.
7. Now you use left and right arrow keys to navigate between the slides.
8. You can also install a plugin called [vim-table-mode](https://github.com/dhruvasagar/vim-table-mode) - this lets you create tables as shown in the image which is a screenshot of a slide

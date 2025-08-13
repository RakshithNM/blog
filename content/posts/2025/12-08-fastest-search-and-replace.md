---
title: Vim search and replace magic wand
date: 2025-08-12
published: true
tags: ['Vim', 'Neovim', 'TextEditor']
description: "Nifty way to search and replace in vim"
---

I found a nice search and replace command in vim. If you need to change all
occurences of a keyword in a file, this is one of the way to do it.

Lets say we have the below text.
```md
Lorem Ipsum is simply dummy text of the printing and typesetting industry.
Lorem Ipsum has been the industry's standard dummy text ever since the 1500s,
when an unknown printer took a galley of type and scrambled it to make a type specimen book.
It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged.
It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages,
and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
```

Now say that you want to change the word `Ipsum` to something else.

You can do it like below
```md
1. Normal mode: /Ipsum
2. Press Enter
3. Type: cgn[WORD] -> replace [WORD] with whatever you want to change it to
   Lets say the [WORD] you want to change to is "India", you would type "cgnIndia"
4. Press Escape
5. Now steps 1 to 4 can be repeated just by the .(dot command)
```

The other way to this is using the substitute command(:s)
```md
1. Normal mode: :s/Ipsum/India/gc
2. Press y for yes on each substitution
```

References: `:help c` `:help gn`

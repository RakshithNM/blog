---
title: Create template code on creating a new file
date: 2025-08-09
published: true
tags: ['Vim', 'TextEditor', 'C']
description: "Quick way to populate new .c files with a 'Hello world!' program."
---

If you are working a lot on a language and are creating many new files, always
having to type the same boiler plate code every time is cumbersome.

To solve this in Vim(Neovim), we can create an auto command to pre populate the file
with some code from a template file.

1. Create a folder, lets call it `templates` in .config folder.
2. Add a file in the language you are working on with some boiler plate code,
   lets call the file `hello` and since I needed it for my C language study
created it with `.c` extension.
3. Fill it with the following code.
```c
#include <stdio.h>

int main() {
  printf("%s", "Hello, world!\n");
  return 0;
}
```
4. Add the below code to your `init.lua` or whereever you see fit.
```lua
vim.api.nvim_create_autocmd("BufNewFile", {
  pattern = "*.c",
  command = "0r ~/.config/nvim/templates/hello.c"
})
```
5. Everytime you open a new file like `vim main.c`, the code in the `hello.c`
   file should populate the `main.c` file.



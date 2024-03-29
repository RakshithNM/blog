---
title: VIM Fun
date: 2022-09-09
published: true
tags: ['Text editor','vim']
cover_image: ./images/vim.png
canonical_url: false
description: "Cool things we can do with vim"
---

VIM is a great tool to master for anyone interfacing with a computer. The documentation is really good and trying to find stuff to read is relatively easy with `:help [keyword]`.
However some of its coolest abilities are not really highlighted and given enough importance. These are some of the less talked about features of VIM(maybe apart from the text-objects, but it's not in `vimtutor`) and how to use them.

# 🐚 Shell Integration
Ex command line(`:help :`), different line range commands and shell integration is one of the most powerful ability of the vim editor. It lets you use all of the UNIX utilities within the editor to transform the selected line range.

Best way to demonstrate this would be using the nifty Unix utility `sort`
```md
1
2
5
6
7
3
4
```
Place the cursor on the first line(on `1`) in the paragraph and press `!}`[For documentation: `:help !` and `:help }`] then type `sort`[For documentation: `man sort`] and press enter. The paragraph is now sorted in the ascending order.

All shell commands can be used including our own bash scripts that can found in path. One such scripts I used pretty often is pasting to online line so as to share code snippets with others. Even though it's out of scope for this article, i'll touch on it here.

## 🔗 Pasting to online paste bin without leaving VIM
1. Create a folder called ~scripts in your home directory.
2. In the directory create a file called ix.
3. Add the following script to the file
```bash
#!/bin/bash

if [ -n "$1" ]; then
  curl "ix.io/$1" 2>/dev/null
  exit 0
fi

curl -F 'f:1=<-' ix.io 2>/dev/null
```
4. Then run chmod +x ix.
5. Add export PATH=$PATH:~/scripts to your ~/.bashrc or ~/.zshrc.
6. Run source ~/.bashrc or source ~/.zshrc.
7. Test that the ix command works by running echo "abc" | ix, it should return a ix.io url.
8. Open up vim and position on top of the paragraph that you want paste online press !} to select the code to ix'ed.
9. Type ix in the bottom where it looks like :.,.+4!, this should return the ix.io url of the form http://ix.io/abcd.
10. Share the url with others.

> NOTE: Visual line selection using (SHIFT-v) and then jumping into command-line mode(pressing `:`) selects all the visual selected lines to be transformed using Unix utilities.
> NOTE: One handy `grep` trick is `grep -v` can be used to do inverse filter.

# 💬 Text Objects
Text objects(`:help text-objects`) are really handy while changing text. If you have a phrase within brackets like `(to change)` that we would like to be changed, and if we have learnt the basic motion commands from `vimtutor` the natural way that most people rely on is
* A) Delete the individual words,
* B) Delete words by count `d2w` while the cursor is on the `(`

and then go into `insert` mode and then insert the desired text.

Text objects make these kinds of text change very easy to do. When you want to change text within `()` to be changed, we can just type `ciw`, this will delete the word within the brackets and put you into insert mode, so you can immediately start typing the new phrase.

This is much better than
- A) because it reduces keystrokes 5(best case) vs 3(any case)
- B) because it elimates(apart from that required to build muscle memory) cognitive load(no more counting of words to be deleted).

For other text objects see `:help text-objects`

Coolest text objects I personally like are:
1. `ciw - Change In Word`
2. `ct{z} - Delete Till Character(should be the letter)`
3. `ci( - Delete In (`
4. `dip - Delete In Paragraph`
5. `cit - Change In Tag (Useful to change content within tag)`

# 🎫 Password Protection/Encryption Of Files
Vim(not Neovim) supports encrypting files. Neovim DOES NOT support encryption of files for reasons mentioned in two links on `:help encryption`.

To encrypt a file open it with `vim -x [filename.extension]`, this will prompt you to enter the encryption key, once it is entered it will put you in insert mode. You can enter the contents of the file, save and quit.

Once we are through this step, opening the file using `vim [filename.extension]` will prompt you to enter the encryption key. `cat`ing the file will show the encrypted form of the file.

# ✍🏻 Editing Files In Compressed Folder
Vim can edit files in a compressed folder!

Let us say we have a folder that has been compressed already and has files in it. You don't have to `unzip` it to edit the file if you use vim.

Just open the folder using vim, it should list all the absolute path of the files, just navigate to the file you want to edit and press enter, if should let you edit. Do the edits and save and quit.

The folder is still in compressed form and the changes you made to the files are saved. You can check this by `unzip`ping and using `cat`.

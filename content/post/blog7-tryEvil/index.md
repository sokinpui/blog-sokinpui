---
title: "Vim emluation on Emacs and Vscode"
#description: <descriptive text here>
date: 2023-06-23T11:24:42+08:00
draft: false
toc: true
image: ""
tags: []
categories: []
---

(Edited date: 2023-06-23T11:24:42+08:00)

Emacs Evil mode, a Vi layer on top of Emacs, in my understanding, Evil is a collection of keys remapping that blinds Emacs function to vi style keys. I love elisp, its powerful expression, the robust ecosystem built on top of elisp, tones of API that help writing my own plugins. I thought it is the most apporach Vim emluation I have tried, if Emacs is start as `emacs -nw`, it will successly pretend Vim TUI!

[Vscode-Neovim](https://github.com/vscode-neovim/vscode-neovim), it uses a fully embedded Neovim instance, so Vscode-Neovim can read the `init.vim` and `init.lua`. Which is really cool, don't have to google the API before configuraion. 

However, I feel the gap when using them. They are great emluation of Vim modal editing, however, other than editing, some important values are still not able to copy, like the integration with shell, and relay on third parity plugin on their ecosystem. Moreoever, I don't feel over advantage to use an emluation than native Vim.

# Emluation can't
`Q` to enter ex mode in Evil.<br>
`q:`, `q?`, `q/`in Vscode-Neovim(extremely useful!)
`sh` in both.(sometimes I want to copy the previous command output)
`term` in Vscode-Neovim to popup an termianl
`:help` in Evil.

---

(edited at Mon Jun 26 12:49:55 PM CST 2023)
# Gravity
Merge to new editor is harder than I thought, I have tried Vscode and Emacs, while they are great editor, but just required sometimes to copy the workflow from my old editor to new editor. Even copied all the keyblindings, some minor but unacceptable difference keep consumming my time to google a solution. For example, the Tab completion style difference between Vscode, Emacs and Vim, I like the popup window of Vim, the tab YouCompleteMe style tab cycling, to get the same setup on Emacs and Vscode are terrible. 

Also, the greatest gravity fallback to the original editor is no productivity gain from switching. If finally I endup with the same writing and editing experience on other editors, I still reach the same level of speed and productivity, then so what? The core of those editor hasn't changed, editing text, maybe Emacs can extand more than editing text. 

After giving a try to those editors, I finally satisify with my current editor. Just be reason when switching tools that have the same functionality in terms of your workflows, especially there is no issue with the current one.

---
title: "Dynamic number-symbol row in vim"
#description: <descriptive text here>
date: 2023-04-07T17:43:58+08:00
draft: false
toc: true
image: ""
tags: ["vim", "keyboard layout", "keyboard", "78% Keyboard"]
categories: []
---
# Abstraction
Provide a way to dynamic swap numbers and symbols in vim according to current 
mode.

# How this idea come
When I write code or writing, I often find the symbols should be easily type as 
single key stroke, while in vim normal mode I find I would like to press number 
in single mode instead of pressing with `shift`. At first, I searched online for 
solution, many of them suggested to swap numbers and symbols, and I agree it may 
convient while coding. However, I am not coding all day, even during coding, in 
vim normal mode something it is handy to use number for `[count]` and command
together. So swapping force you to choose one of them for more convenience
typing. Another solution is to use number pad layer, I would say it is same as
swapping, since I have to press with another key to use numbers, the problem
havn't been solved.

One day, When I was editing code, the idea of toggling nubmer-symbol row come in
my mind, then I implement it, and find it solve the problem quite well regarding
not prefect.

# Number-symbols toggle
Well, it is actually a dead key leader, when I press the `toggle key` which is
`equal sign` of my keyboard. The nubmer row will swap to symbol row, press
again, back to number.

# Dynamic Number-symbols row in vim
Since vim is modual, when insert mode, I prefer using symbols over numbers, when
normal mode, I prefer the opposite. Then I add some rules for the toggle keys.

Back to normal mode, which is equivalent to press the `esc` key, so when press
`esc` key, define `nst` to False. It means toggle number rows. 
```
[:escape :left_control nil {:alone [ ["nst" 0] ["n-layer" 0] :escape  ]} ]
```
The above snippets is goku code, a config layer on top of [Download 
Karabiner Elements](https://karabiner-elements.pqrs.org/), which is a tools for
Mac to remap keyboard layouts.

Enter insert mode, is equivalent to `a`, `i`, `s`, `A`, `I`, `S`, `o`, `O`, `c`,
`C`. Then turn `nst` to True when type those key.
```
[:i                           [:i  ["nst" 1]]]   
[:a                           [:a  ["nst" 1]]]   
[:s                           [:s  ["nst" 1]]]   
[:c                           [:c  ["nst" 1]]]   
[:o                           [:o  ["nst" 1]]]   
```
The above code define `nst` to True when type `i` ( not `I` ).

Furthur more, there is a few more situation I would prefer symbols over number,
they are searching and command mode. Then I add those lines also.
```
[:semicolon                   [:semicolon ["nst" 1]]]   
[:slash                       [:slash ["nst" 1]] ]
```

# Inprefect
Since the layer is define outside vim, it can not avoid symbols row toggle
during normal mode, when I type `yip` in normal mode, the symbol row toggle.
Although I can have some line like `inoremap 1 !` and `cnoremap 2 @`, I don't
want to pollute my mapping to much, I give up to implement this in pure vim way.
I am interesting to find how to let karabiner know that I am in vim normal mode,
so that avoid toggle symbol row accidently.

I have remap `equal sign` to the `caps lock`, so it is possible for me to have
one dead key, if you want to implement also, you may find your own.

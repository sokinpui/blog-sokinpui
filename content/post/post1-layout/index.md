---
title: "Desisgn of Keyboard Layout on standard 78% keyboard"
#description: A personal defined MacBook Keyboard.
date: 2023-03-26T19:23:56+08:00
draft: false
toc: true
image: ""
tags: ["keyboard", "Macbook"]
categories: []
---

## Abstruct
2023 is a start of AI era, with more strong AI tools explore to our life, typing 
maybe replaced by voice input one day, where natural language programming become 
true. But until now, typing is still not replacable. From daily usage to 
programming, the location of the keys may significantly effect the comfortable 
of long time typing. Here is a brief solution that hope to enhance the 
experience when typing on standard 78% keyboard.

## Reason to redesign.
I use Macbook Air as my main machine, stick to it and cannot use an customizable 
keyboard like **planck's keyboard** and **hhkb keyboard** for the desire of 
protable. The plain of using standard 78% keyboard on Macbook is the overusage 
of pinky, `Backspace`, `[`, `]`, `-`, `=` and `Enter` are all handled by right 
pinky. As my right pinky is much weaker than left, which make typing long time a 
difficult, inefficient and tired task. I believe it is true for other user who 
programming a lot with Macbook.

There are so many plans and existing well designed layouts on the Internet, 
while they are mainly for one who use a external non-standard keyboards instead 
of standard. So I hope there will be more disscusion about configuration of 
trivail standard keyboard.

## Choose of base layer, Qwerty
Not Colemak, Dvoark and any non-Qwerty. I have tried Colemak and Dvoark, but the 
musale memory of Qwerty is too strong that make me feel more natural and 
comfortalbe typing on Qwerty. Moreover, the change of layout may not bring 
significant advantages and comfor for typing, 10 keys on homerow is never 
enough, whatever layouts, your fingers still need to move along three rows to 
type characters. The analysis of those Qwerty alternative always be to ideal, 
without mention of muscale memory and symbols make such change not really solve 
the plain. Another reason is that the time cost is too high and the improvement 
is not that big, there is not need to explain why the time cost is high as it is 
well explained by those Qwetrty touch typer how share their experience of 
switching to non-Qwerty.

## Analysis before design
Except the function row, all row is easier to reach even for number rows. I 
don't touch type numbers rows using pinky fingers. Instead, I use ring fingers 
which are much longers then pinky fingers. So the keyboard layout don't need to 
relay on layers heavily like 40% planck's keyboard.

Let counts the key we need:
1. 30 characters on the main area of the keyboard including `,`, `.`, `/` and 
   `;`.
2. 13 keys on numbers
3. 8 modifier keys, `capslock`, `left right option`, `left right command`, `left 
   shift`, `control`, `fn` I don't count right shift since I never use it.
4. 4 special keys, including `space`, `reutrn`, `tab` and `delete`.
5. 4 arrow keys, I don't want to use home row arrow keys, since I seldom use 
   them, there is no need to prepare a layer for them.

61 keys is already sweat enough for daily used, for those shortcut, I usually 
reduce them from three or above keys into two keys by define a customizing 
layer.

## Layers
There are two types of layers, dead keys and modifers

### Dead keys
The layout of keyboard is chagned permanently untill you press other keys or the 
inactive keys. One of the exmaple are the comma of 
[workman-dead](https://github.com/workman-layout/Workman/tree/master/mac).

### modifers
The layout is changed temporary, the layout return to default after release. One 
of the example is `shift`.

### My solution
There are some keys that is underused, like space, tab and return. There are 
much space that can be leveraged. They should perform tap-mode, which provide 
two funciton when tap and held them down.
1. Remap `space` to `space` when tap, `shift` when held.
    It is much comfortable compare to use pinky finger to press shift.
2. Remap `left shift` to `escape` when tap, `control` when held. I use vim.
3. swap numbers and symbols for programming.
4. remap `caps lock` to `=` when tap, switch layer when held.
5. swap quote `'` and double quote `'`, and locate at the original position of 
   open bracket.
6. move hyphen and underscore to the original position of quote.
7. move backslash and pipe to the original position of hyphen.

**Layers:**<br>
caps lock layers(held down caps lock):<br>
u: ]<br>
i: [<br>
j: }<br>
k: {<br>

### Macro sequences
You can define a simple key that perform a sequence of key. It is better put 
them in a layer to avoid error when typing.<br>
I have defined some in the caps lock layer.<br>
d: -><br>
f: !=<br>
:: @:<br>

## Implementation
You may wonder how to implement those change on Mac, you may use [Karabiner 
Elements](https://karabiner-elements.pqrs.org/) together with 
[Goku](https://github.com/yqrashawn/GokuRakuJoudo) to define your own keyboard 
layout.

## Conculsion
There are lots of method to increase comfortable and efficiency to get the job 
done, before typing to modify your keyboard, make sure you have tried to use 
**good tools** like Vim, IDE, auto compeletion, snippets and scritping to 
reduece typing. Single modification of keyboard won't make you a better typer.  
With the help of snippets and auto completion, I now write code with less demand 
to type all the symbols manually, therefor a entire symbols layers on homerow is 
no needed(Previously I have one, use space to active, convert home row into 
common used symbols.)



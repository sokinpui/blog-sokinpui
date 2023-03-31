---
title: "Define layer using Karabiner Elements togther with Goku"
#description: Explanation of layer implementation in Karabiner Elements.
date: 2023-03-31T17:27:25+08:00
draft: false
toc: true
image: ""
tags: ["goku", "Karabiner Elements", "keyboard"]
categories: []
---

If you don't know the basic syntax of Goku, please see the [offical
tutorial](https://github.com/yqrashawn/GokuRakuJoudo/blob/master/tutorial.md).

# What is Karabiner Elements?
Karabiner Elements is a keyboard modifier on MacOS, which support key blindings 
remap and define layer, or in another form, complex modification. [Download 
Karabiner Elements](https://karabiner-elements.pqrs.org/).

# What is Goku?
Goku is a config file that ease the configuration in Karabiner Elements. In 
Karabiner Elements, if you want to implement complex modification, you will need 
to edit the json file, which is wired, it is very likely loss for beginners who 
don't know the sturcture of modification of Karabiner Elements. Also, time is 
limited, why don't use an easier tools that already on top of Karabiner Elements 
to make life easier? [Goku on 
github](https://github.com/yqrashawn/GokuRakuJoudo)

# Define your customized layer
## 1. Why define layer
The functionality of keyboard can be exteneded, one way is to define your own 
layers. With layers, you can shorten the key blindings in some "shortcut" 
usually require pressing three to four keys together. Or build an symbols layer 
if you stuck in the current `number + shift` way.

## 2. Different types of layers
### Traditional layers
Traditional layers like the layers of QMK mod-tap feature, a key's function is 
divide into two, when you held down, it is modifier, and you loss its tap's 
function, and vice verse.

### Simlayers
In Goku, **simlayer**(simultianeous-layer) differ from traditional layers which 
you would not loss key's original fucniton. **For example, if you define `f` as 
your simlayer, if you held down `f`, stream of `f` will be inserted. Conversely, 
if you define `f` as tranditional layers, no `f` is insertd even you held it 
down.** 

In the 
[tutorial](https://github.com/yqrashawn/GokuRakuJoudo/blob/master/tutorial.md) 
of goku, author states the problems of traditional layers. But to me, they are 
the benefits, since simalayer have delayed display and require really fast right 
key followed. So, in this page, I would suggest you to use traditional layers.

# Implement layers with Goku
## 1. define variables.
Variable help karabiner element know the state of your keyboard to act in 
performs different events in each states.

```python
["name of variable" 0/1]
```
It is a sturcture of variable, doble quoted name, 0 or 1 state.

```python
[:fookey   ["foovar-set" 0/1]   ["foovar-cd" 0/1]]
```
It is conditional event, the last one is the condition, the middle one is `to 
event`, which set `foovar-set` to 0 or 1 if the condition is met.

```python
[:fookey   [["foovar1" 0/1] ["foovar2" 0/1]]     ["foovar" 0/1]]
```
It is same strcture of above but with extended `to event`, which set two 
variable in sequence, the condition part can also be extened in vector `[["foo1" 
1] ["foo2" 1]]`, vector can expand as much as you want.

## 2. mod-tap Layers
This type of layer active if you held down fookey. inactive if you release.
```python
[:w ["tap_fookey" 1] nil {
 :alone [:w]
 :afterup ["tap_fookey" 0]
:tap_fookey
[:period  :1  ]
```
The first `["tap_fookey" 1]` is the key event if you held down, `alone` is the 
key event if you tap single. `:afterup` is after key up event. The last line 
`:tap_fookey` tells karabiner to perform the following events if `"tap_fookey"` 
is met, In this example, it is `w+. -> 1` it is like the conditions.

## 3. dead keys
This type of layer active if you press fookeys, inactive if you press the 
fooleavekey.
```python
[:fookey            ["dead_foo" 1]]
[:fooleavekey       ["dead_foo" 0]]
:dead_foo
[:foo_from       [:foo_to ["dead_foo" 0]]]
[:foo_from       :foo_to ]
```
Dead key is actually a simple layer checked with variales state, the first event 
in dead_foo will leave layer after press the `foo_from`, while the second 
won't.<br>
If you wish to leave the layer with the same keys you can:
```python
[:comma  ["taped" 0]  ["taped" 1 ] ]
[:comma  ["taped" 1]  ["taped" 0 ] ]
:taped
[:period  :1  ]
```

## double tap layer
```python
;; check double tap
[:right_shift  ["two" 1]  ["one" 1]]

;; chekc single tap
[:right_shift :right_shift nil
    {:alone  [:right_shift ["one" 1]]
    :delayed {:invoked ["one" 0] :canceled ["one" 0]}
    :params {:delay 1000}}]

:two
[:period  :1  ]
```
This layer keep the function of `right shift`, but I don't know why it fail to 
use `right shift` to escape.<br>
The single tap check is a little bit complicate, nil is introduced in mod-tap 
layer which extended the `to event`, new `:delayed` control the behaviour after 
the key tapped, `:invoked` and `:canceled` work as their name.  `:params {:delay 
1000}` denote the time for the accepted delay time, `invoked` event trigger 
before that time, `canceled` event trigger after that time.<br>
**The double tap check should be put before single tap check.**<br>
To escape the layer use the same key use the follow snippet instead:
```python
    ;; check double tap
    [:right_shift  ["two" 1]  ["one" 1]]
    
    ;; chekc single tap
    [:right_shift [:right_shift ["one" 1]] ["two" 0]
        {:delayed {:invoked ["one" 0] :canceled ["one" 0]}
        :params {:delay 1000}}]

    :two
    [:right_shift  ["two" 0]]
    [:period  :1  ]
```
It first check that if right_shift is tap twice and once, and leave if tap twice 
already. But this cannot perserve the function of `right shift`, so it cannnot 
be act like modifier anymore, to be noted, the last example that perserve `right 
shift` can replace by othey with variables, so as mod-tap layer and double 
tapped layer at the same time.

## Marco
This is actually not a layer, but a collection of keys. I have defined a layer
to shorten repetitive keys sequence into single press.
```python
[:i     [:i :n :s :e :r :t :spacebar :a :spacebar :j :o :k :e]] 
```
Which will insert `insert a joke` with space if you press `i`.

## My karabier.edn
Here is a 
[reference](https://github.com/sokinpui/config/blob/main/karabiner.edn) for your 
own implementation.

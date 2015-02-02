---
layout: post
title: "Week 2: Emacs and Collatz"
date: 2015-02-01 16:10:31 -0600
comments: true
categories:
---

We are now in our second week of class and have been given the first assignment: Collatz.
The assignment is to write a program that finds the maximum cycle length of a range specified by user input.
After finishing, we are expected to submit our assignments to [SPOJ](http://www.spoj.com/problems/PROBTNPO/)
As mentioned before, I've already taken one of Downing's classes, Object Oriented Programming.
Luckily, the first assignment is the same, albeit with some differences.
As such, I finished this assignment quite quickly.
The lectures were familiar to me as well. He used the same examples, same code, and even the same jokes.
As such, I found myself bored with most of the material. Rather than succumbing to apathy, however, I greeted an old friend of mine: Emacs.

I first met Emacs nearly three years ago.
At that time, I was a Vim enthusiast.
My setup included dozens of plugins, ranging from [eclim](http://eclim.org/) to [Tabular](https://github.com/godlygeek/tabular).
I was an avid [Vim Golfer](http://www.vimgolf.com/) and sported a complex workflow involving sending Vim text objects to Tmux sessions.
I demanded that my entire system used Vim bindings, installing [Vimperator](http://www.vimperator.org/vimperator) and rebinding GMail keystrokes.
At that time, I believed that Vim was superior to other editors.
I would sneer at the other Freshman using Sublime and TextMate while I wrote obstruse regex.
However, after seeing Matz, the creator of Ruby, give a talk about his experience with Emacs I was inspired to do the same.

For the next few weeks, my pinky was aching from overuse.
Initially, I struggled with Emacs, often cursing it's default bindings.
Everytime I installed a new plugin, I was forced to learn a myriad of new commands.
C-c M-p f, C-M-p f, C-p M-c f. My fingers became adept at acrobatics.
Furthermore, these bindings are dynamic.
Depending on the modes of the buffer, which are sourced from file name and type, these bindings could have an entirely different meaning.

Yet, I continued to use Emacs. The reason being Lisp.
Vim is configured through its own language, Vimscript.
Vimscript is renowned for its various misgivings.
For example,


``` vim Whitespace at the end
nnoremap Z zz
nnoremap Z zz
```


See the difference between the two lines?
It's a single whitespace at the end.
Vimscript treats everything as a string, and as such, whitespace is significant.
The difference between the two can be disastrous at times.
This is only one of the many hacks Vimscript contains.

Emacs, on the other hand, uses Emacs Lisp.
Although Lisp was frightening at first with its mountains of parentheses, I came to slowly appreciate the design and elegance of the language.
Emacs is often joked about being an OS rather than a text editor, and to a degree, I think that statement's true.
Emacs has proper asynchronous operations and has a myriad of plugins, including a web browser, email and even tetris.
Users can rewrite nearly any aspect of the editor fluidly and consistently.
As such, the plugins that have emerged are simply amazing.

Evil is a near complete emulation of Vim keybindings.
Magit is a unique interface to git that is worthy of being its own application.
Flycheck is a robust syntax checker that runs quickly in the background without any delay.
Jedi is an interface to the Python Jedi server that offers code completion on par with fully-featured IDEs.

Now, I think it's unfeasible to drop emacs for any other editor.
If some new IDE offers a unique feature, it's likely that someone will make a similar plugin for emacs in a matter of months.
If a certain aspect of the GUI bugs me, I can customize it as I wish or even delete it entirely.
I've been with emacs for three years now.
Along the way, I've written thousands of lines, learned new langauges, and became faster at programming.
As I've changed, emacs has changed with me as well.
More than an editor, it's a lifetime partner.

{% img http://i.imgur.com/J3lui9F.png %}

Thanks for reading,
Paul

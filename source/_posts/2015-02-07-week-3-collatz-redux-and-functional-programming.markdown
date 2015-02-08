---
layout: post
title: "Week 3: Collatz Redux and Functional Programming"
date: 2015-02-07 19:12:59 -0600
comments: true
categories: 
---

The Collatz assignment was due this week, and much to my dismay, I don't think I
did too well. The main problem was in [V2](http://www.spoj.com/problems/PROBTRES/), the extra credit option available to
us. 

This new version had the same specifications as the [original question](http://www.spoj.com/problems/PROBTNPO/), 
but had differing input. The two differences with this version are:

1. Input contains empty newlines. 
  Professor Downing gave us the framework for the code, and input/output was
  included in this framework. The only thing we needed to implement was a method
  of the following definition: `def collatz_eval(x, y)`
  So, when receiving numerous runtime errors on Sphere, it didn't occur to me to
  fix the input function. I was rather narrow-minded in my debugging and I
  wasn't able to find the bug in the end. I'm humbled from the experience and
  determined to not err the same way again.

2. Output can overflow a 32-bit unsigned int and the result should be overflowed
  I managed to figure this one out by successfully writing code that lead to
  correct results in C++. The solution was rather simple: bit anding with the
  max 32-bit value every iteration.

In total, I'm disapppointed in myself for this project. I admit I was arrogant
coming into it and failed to properly consider the requirements at hand. I
learned a valuable lesson from this project and it is one that I hope to never
forget.

Moving forward, the lectures for this week were among the most interesting so
far. We covered my favorite topic in Python: functional programming!

Functional programming offers many benefits, conciseness, ease of development,
and reliability. One that I was surprised to find in Python was the increased
speed. I tested this in IPython with the following:

```python
>>> words = ["string"] * 1000
>>> %timeit map(str.upper, words)
# 1000000 loops, best of 3: 265 ns per loop
>>> %timeit [x.upper() for x in words]
# 10000 loops, best of 3: 128 µs per loop
```

That's nearly a thousand times speedup. The main reason being that map pushed a
for loop from the interpreter into C code, thus speeding up the disassembly.
However, it's not significant in real-world code and list compehrensions are
much more common in use.  [This](http://stackoverflow.com/questions/1247486/python-list-comprehension-vs-map) 
is a really good post about the differences between the two.

Regardless of speed, however, functional programming does offer many benefits.  
It's a different way to approach problems and it enables for clever and
beautiful solutions. Without a doubt, functional programming is a useful tool
for any programmer and I'm ecstatic to see what Python will offer.

Thanks for reading,
Paul

---
layout: post
title: "Week 4: Tricky Generators"
date: 2015-02-15 14:52:14 -0600
comments: true
categories:
---

This week, we continued our adventure into functional programming and talked
about an interesting feature of Python: Generators.
Generators are functions that behave as iterators, thus enabling them to be used
in loops. A prime example of this would be in Haskell, where everything is a
generator.

```haskell
fibs :: [Integer]
fibs = 1:1:zipWith (+) fibs (tail fibs)
```

Tada! A lazily-evaluated infinite list. If we were to do something similar in Python, we would get:

```python
def lazy_fibb():
    a, b = 1, 1
    while True:
        yield a
        a, b = b, a + b
```

The benefits of Python's approach is no doubt it's readability.
We can easily see the mechanics of the function and the result it gives.
In comparison to more rigid functional languages, which normally require experience and time to understand, Python's generators are quite elegant.

On a side note, Professor Downing gave us the first trick question of the semester.

```
print(for x in range(100))
```

What would the above print?
Well, although I held doubts about the syntax, I put down the expected answer of the integers from 0 to 99.
Yet, I was dismayed to find out that the answer was "generator 0x1abc0ed"

I suppose it's a good wake up call to pay more attention to the specifics of the code.
I tend to avoid being picky with syntax, instead trying to infer the general logic behind the code.
Yet, certain cases do call for it and it seems like I need to pay closer attention.

A close friend of mine partnered up with me to do the Netflix assignment and he was intrigued by IPython.
IPython is a shell, similar to what python does when invoked with no arguments, and offers a plethora of benefits.
One of my favorite features is the timeit "magic" call.

```python
>>> %timeit sum(range(100))
...
>>> %timeit reduce(operator.add, range(100))
...
```

other features include auto-completion, bash commands (ls and cd), integration with pdb, automatically inserted parentheses, and a variety of "magic" functions.
I'd recommend giving it a shot.

Thanks for reading,
Paul

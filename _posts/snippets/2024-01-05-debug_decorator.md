---
title: The Debug Decorator
date: 2024-01-05 17:45:00 -0500
categories: [Snippets, Code]
tags: [python, code]
---
A decorator is a function or a class that wraps (or decorates) a function or a method, modifying their coded behaviour.

A simple definition:
> Decorator is a design pattern that attaches additional responsibilities to an object dynamically.[^design]
{: .prompt-info}

Decorators are useful for separating external logic from polluting the core logic of the function.[^debug]

## Code
```python
import functools

def debug(func):
    """Print the function signature and return value"""
    @functools.wraps(func)
    def wrapper_debug(*args, **kwargs):
        args_repr = [repr(a) for a in args]                      # 1
        kwargs_repr = [f"{k}={v!r}" for k, v in kwargs.items()]  # 2
        signature = ", ".join(args_repr + kwargs_repr)           # 3
        print(f"Calling {func.__name__}({signature})")
        value = func(*args, **kwargs)
        print(f"{func.__name__!r} returned {value!r}")           # 4
        return value
    return wrapper_debug
```
Decorators are a powerhouse when it comes to reusing functionality across multiple objects. The above debug
decorator can wrap around all functions and methods in your project to make debugging a cakewalk.

If you're confused about the wrapper function nested within the decorator, here's a thread that might help.[^stack]

## Final Thoughts
Decorators have more fancy usecases to be explored, hopefully in a future post. Meanwhile, here's a video introduction
to the concept.[^yt]
{% include embed/youtube.html id='r7Dtus7N4pI?si=ugqf2iwIFjPfusta' %}

## Resources
[^debug]: [Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/#debugging-code)
[^design]: [Medium - Why do we need decorators? Use cases.](https://medium.com/exness-blog/why-do-we-need-decorators-use-cases-13f19ca5d237)
[^stack]: [Why do we need the wrapper function in decorators?](https://stackoverflow.com/questions/45335580/why-do-we-need-wrapper-function-in-decorators)
[^yt]: [YouTube ➡ Python decorator in 10 mintues](https://youtu.be/r7Dtus7N4pI?si=JAp1COWJX3eN5ISF)
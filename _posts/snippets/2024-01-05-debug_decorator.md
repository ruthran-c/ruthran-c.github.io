---
title: The Debug Decorator
date: 2024-01-05 17:45:00 -0500
categories: [Snippets, Code]
tags: [python, code]
---

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
[^debug]

# Resources:
[^debug]: [Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/#debugging-code)
---
title: The Walrus Operator in Python 3.8
date: 2023-09-13 01:27:00 +0530
categories: [Snippets, TIL]
tags: [python]
---

Python 3.8 brought about a new assignment expression that trims your length of code and improves readability.

Let me explain how:

## The Operator
`:=` ➡ The walrus operator assigns values to variables as part of a larger expression[^walrus].

> The use of the walrus operator should be limited to clean cases that reduce complexity and improve readability.
{: .prompt-warning}

## Usage
In this example, the operator helps avoid calling len() twice or defining n outside the loop in vain:
```python
if (n := len(a)) > 10:
    print(f"List is too long ({n} elements, expected <= 10)")
```

But overall, the **main use case** for which I've been dreaming about the existence of this operator is 
for list comprehensions:
```python
[clean_name.title() for name in names
if (clean_name := normalize('NFC', name)) in allowed_names]
```
Where a value computed in a filtering condition is also needed in the expression body.


## Resources
[^walrus]: [What’s New In Python 3.8 ➡ New Features ➡ Assignment expressions](https://docs.python.org/3/whatsnew/3.8.html#assignment-expressions)
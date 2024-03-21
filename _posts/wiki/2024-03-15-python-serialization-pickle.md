---
title: Serializing Python Objects using Pickle
date: 2024-03-15 11:45:00 -0500
categories: [Wiki]
tags: [python]
---

[Pickle](https://docs.python.org/3/library/pickle.html) is the native data serialization module for Python.[^hitch]
It is the simplest and most effective way for storing and sharing Python data in the short-term.

## Data Serialization
It is the process of converting structured data into a format through which storing and sharing of the data is possible.
Without serialization, the data would be force converted into a str, where the  

> The serialized data can be recovered to its original structure.

Some of the other common serializing methods are:

|   Flat data    |  Nested data  |
|:--------------:|:-------------:|
|     `repr`     |    `YAML`     |
|     `csv`      |    `JSON`     |
| `NumPy Array`  |     `XML`     |


## Code
```python
import pickle
with open('file.pkl', 'rb') as f:  # The 'b' stands for byte.
    data = pickle.load(f)

with open('file.pkl', 'wb') as f:
    pickle.dump(data, f)
```

## Resources
[^hitch]: [The Hitchhiker's Guide to Data Serialization.](https://docs.python-guide.org/scenarios/serialization/)
[^datacamp]: [DataCamp - Pickle Python Tutorial](https://www.datacamp.com/tutorial/pickle-python-tutorial)
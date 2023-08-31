---
title: Convert Ragged Nested Sequences to MultiIndex Pandas DataFrame
categories: [Snippets, Code]
date: 2023-08-31 23:43:00 +0530
tags: [python, pandas]
---

## What's a Ragged Nested Sequence? 
A ragged nested sequence is defined in Python as 
`a list-or-tuple of lists-or-tuples-or ndarrays with different lengths or shapes`.

Essentially it's an array of arrays where the sub-arrays are of different lengths.

```python
[
    [
        ['high', 'med', '3', '2', 'med', 'low'],
        ['med', 'low', '5more', '2', 'big', 'med'],
        ['vhigh', 'vhigh', '2', '2', 'med', 'low'],
        ['high', 'med', '4', '2', 'big', 'low']
    ],
    [
        ['med', 'low', '3', '4', 'med', 'med'],
        ['med', 'low', '4', '4', 'med', 'low'],
        ['low', 'low', '2', '4', 'big', 'med']
    ],
    [
        ['med', 'vhigh', '4', 'more', 'small', 'high'],
        ['med', 'med', '2', 'more', 'big', 'high'],
        ['med', 'med', '2', 'more', 'med', 'med']
    ]
]
```
{: .nolineno file="Ragged Nested List" }
> This example was taken from a decision trees tutorial's cars dataset.

## Why convert it into a DataFrame?
- It's difficult to work with in list form.
- The sequence cannot be converted to ndarray directly since the lengths are unequal.
- Visualization of the data is non-optimal.

## Code
```python
...

inner_length = [len(split) for split in data]
keysOuter = []
keysInner = []

# keysOuter contains outer index (outer split) for all rows.
# keysInner contains inner index (numbering).
for ind in range(len(inner_length)):
    for i in range(inner_length[ind]):
        keysOuter += ['split' + f'{ind+1}']
        keysInner += [i]

# Create a flat DataFrame without hierarchy.
df = [item for row in data for item in row]
df = pd.DataFrame(df)
df['outer'] = keysOuter
df['inner'] = keysInner
# Set MultiIndex.
data = data.set_index(['outer', 'inner'])
```

## DataFrame

| <br/>outer | <br/>inner | 0<br/> | 1<br/> | 2<br/> | 3<br/> | 4<br/> | 5<br/> |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| split1 | 0 | high | med | 3 | 2 | med | low |
|  | 1 | med | low | 5more | 2 | big | med |
|  | 2 | vhigh | vhigh | 2 | 2 | med | low |
|  | 3 | high | med | 4 | 2 | big | low |
| split2 | 0 | med | low | 3 | 4 | med | med |
|  | 1 | med | low | 4 | 4 | med | low |
|  | 2 | low | low | 2 | 4 | big | med |
| split3 | 0 | med | vhigh | 4 | more | small | high |
|  | 1 | med | med | 2 | more | big | high |
|  | 2 | med | med | 2 | more | med | med |

## Final Thoughts
If you code in `df.index`, you get a MultiIndex output:
```output
MultiIndex([('split1', 0),
            ('split1', 1),
            ('split1', 2),
            ('split1', 3),
            ('split2', 0),
            ('split2', 1),
            ('split2', 2),
            ('split3', 0),
            ('split3', 1),
            ('split3', 2)],
           names=['outer', 'inner'])
```
{: .nolineno file="Output" }
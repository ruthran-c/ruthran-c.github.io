---
title: Aggregating categories using masks
#date: 2024-01-21 09:30:00 -0500
categories: [Snippets, Code]
tags: [python, pandas]
---

```output
Liliana    1067
John        998
William     494
Emilie      196
Pattie        6
Neil          3
Bob           2
Demi          1
David         1
Hester        1
Name: Vote, dtype: int64
```
```python
# election_data is the DataFrame
# get the counts for each candidate
votes = election_data['Vote'].value_counts()
mask = election_data.isin(votes[votes < 200].index)
election_data[mask] = 'Other'
```
```output
Liliana    1067
John        998
William     494
Other       210
Name: Vote, dtype: int64
```

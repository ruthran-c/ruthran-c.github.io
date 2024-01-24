---
title: Combining categories using masks
#date: 2024-01-21 09:30:00 -0500
categories: [Snippets, Code]
tags: [python, pandas, eda]
---
When working with categorical data, simplifying the analysis is often beneficial 
by either combining or eliminating less significant categories. 
This might arise due to the rare frequency of said categories in our data.

Therefore, EDA streamlining can be achieved by consolidating these categories 
into a uniform "**Others**" category.

Take a Series containing the number of votes recorded for each candidate:
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
All the candidates below our "**Emilie**" candidate are insignificant due to the minimal number of votes. So we can combine them
into a cohesive "Others" category.

## Code
```python
# election_data is the DataFrame
# get the counts for each candidate
votes = election_data['Vote'].value_counts()
other = list(votes[votes < 200].index)

mask = election_data.isin(other)
election_data[mask] = 'Other'
```

You can also stack the DataFrame, compare the DF against the scalar value, 
replace and unstack for final result.[^stack]
```python
stack = df.stack()
stack[stack.isin(other)] = 'Other'
election_data = stack.unstack()
```

Or, you could go with the normal `pd.replace` route:
```python
votes = election_data['Vote'].value_counts()
df = df.replace(votes, 'Other')
```

The `value_counts()` then becomes:
```output
Liliana    1067
John        998
William     494
Other       210
Name: Vote, dtype: int64
```

## References:
[^stack]: [StackExchage](https://stackoverflow.com/questions/42276396/typeerror-cannot-do-inplace-boolean-setting-on-mixed-types-with-a-non-np-nan-va)

---
title: Itemgetter & 'key' arg in Max() 
categories: [Snippes, TIL]
---



```python
max(
      tree.labels.items(), 
      key=operator.itemgetter(1)
      )[0]
```
---
title: Itemgetter & 'key' arg in Max() 
categories: [Snippets]
tags: [python, toolkit]
---

```python
max(
      tree.labels.items(), 
      key=operator.itemgetter(1)
      )[0]
```
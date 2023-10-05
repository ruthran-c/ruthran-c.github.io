---
title: Jupyter notebook customizations
date: 2023-10-05 16:41:00
categories: [Snippets, Toolkit]
tags: [python]
---

### Print all cell outputs

```python
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```
{: .nolineno}

## Resources
- [IPython ➡ Terminal IPython options](https://ipython.readthedocs.io/en/stable/config/options/terminal.html)
- [How to Effortlessly Optimize Your Jupyter Notebook.](https://towardsdatascience.com/how-to-effortlessly-optimize-jupyter-notebooks-e864162a06ee)
- [Why I love using the IPython shell and Jupyter notebooks](https://opensource.com/article/21/3/ipython-shell-jupyter-notebooks)
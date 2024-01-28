---
title: Wrap Graph Labels in Matplotlib
date: 2024-01-28 120000 -0500
categories: [Snippets, Code]
tags: [python, matplotlib, seaborn, code]
---

Overlapping text labels on the x-axis is a common challenge during visualizations. 
To mitigate, we can rotate the labels by an angle to create more space, 
implement text wrapping for multi-line visibility, or combine both:

## Code
```python
import textwrap
def wrap_labels(ax, width, break_long_words=False):
    labels = []
    for label in ax.get_xticklabels():
        text = label.get_text()
        labels.append(textwrap.fill(text, width=width,
                                    break_long_words=break_long_words))
    ax.set_xticklabels(labels, rotation=30) # Change the rotation to suit preferences.
```
This provides clearer visualizations of our data.

## Plots
|                                           Before Text Wrap                                           |                                           After Text Wrap                                            |
|:----------------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------------:|
| ![text_wrapped_dark](20240128-light1.png){: .light}![text_wrapped_dark](20240128-dark1.png){: .dark} | ![text_wrapped_dark](20240128-dark2.png){: .dark}![text_wrapped_dark](20240128-light2.png){: .light} |



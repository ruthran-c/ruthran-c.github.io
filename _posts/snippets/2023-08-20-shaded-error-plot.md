---
title: Time Series Plot with Shaded Error Region
date: 2023-08-20 16:00:00 +/-TTTT
categories: [Snippets, Code]
tags: [code, python, plots, pics]
---

```python
...
ax = plt.subplot()

ax.set_xticks([iter for iter in hour if iter % 2 == 0])
ax.set_yticks([0, 20, 40, 60, 80, 100, 120])

y_upper = [i + (i * 0.15) for i in viewers_hour]
y_lower = [i - (i * 0.15) for i in viewers_hour]

plt.fill_between(hour, y_lower, y_upper, alpha=0.2)
plt.show()
```
{: .nolineno }

![error as shaded region in time series plot](/snippets/20230820-colorShade.png){: .light}
![error as shaded region in time series plot](/snippets/20230824-colorShade-dark1.png){: .dark}
_Time series plot with shaded error region_
---
title: Dark-Mode Images for Chirpy Jekyll Pages
date: 2023-08-23 10:14:00 +0530
categories: [Snippets, Code]
tags: [code, python, plots]
---

## Background
The Chirpy template allows you to input 2 separate images in posts and
be able to display only the image that corresponds to the light/ dark mode currently set.

You can do this by adding a **block IAL** to the image block with
either `:light` or `:dark`.

```markdown
![Light mode only](/path/to/light-mode.png){: .light }
![Dark mode only](/path/to/dark-mode.png){: .dark }
```
{: .nolineno}

## Goal
Customize image settings in Python that seamlessly produces dark mode images for Chirpy.

- The facecolor of the image (background color) should be the same as Chirpy's dark background.
- The facecolor of the axes (space in b/w the axes) should be a little different to contrast
  the image with the background.

## Code
```python
fig = plt.figure(facecolor=("#1b1b1e"))
plt.style.use('dark_background')

...

ax = plt.subplot()
# ax.set_facecolor((.44, .45, .45))

...

plt.show()
```
{: .nolineno}

## Final plot
You get a plot that seamlessly merges into the background while the facecolor between the axes
comes from the `dark_background` style. You can uncomment`ax.set_facecolor()` 
to override a lighter shade for the graph.

![Dark mode plot](20230824-colorShade-dark1.png){: .dark }_Image only displayed in dark mode_

### Multiple images side-by-side
When you want multiple images side by side, we need to use tables and set each image as a cell. 

Chirpy has customized different colors for the cell blocks. Hence we make small changes 
to the plot's facecolor. The best fit I found to date is `#2A2F35` for `plt.figure()`

|                                       `dark_background`                                       |                              `ax.set_facecolor((.44, .45, .45))`                               |
|:---------------------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------------------:|
| ![Dark mode plot](20230824-colorShade-dark3.png){: .dark }_Image only displayed in dark mode_ | ![Dark mode plot](20230824-colorShade-dark4.png){: .dark }_Image only displayed in dark mode_  |


## Learn More
1. ["Adding multiple attributes with Kramdown"](https://www.stevefenton.co.uk/blog/2022/09/adding-multiple-attributes-with-kramdown/) 
by Steve Fenton.
2. Markdown renderer supported by Jekyll - [Kramdown](https://jekyllrb.com/docs/configuration/markdown/#kramdown).
---
title: Customize a dark mode image for Chirpy Jekyll pages
date: 2023-08-24 10:14:00 +/-TTTT
categories: [Snippets, Code]
tags: [code, python, plots]
---

## Background
Currently, the Chirpy template allows you to input 2 separate images in posts and
be able to display only the image that corresponds to the light/ dark mode currently set.

You can do this by adding a **block IAL** to the image block with
either `:light` or `:dark`.

```markdown
![Light mode only](/path/to/light-mode.png){: .light }
![Dark mode only](/path/to/dark-mode.png){: .dark }
```

## Goal
Customize image settings in Python that seamlessly produces dark mode images for Chirpy.

- The facecolor of the image (background color) should be the same as Chirpy dark background.
- The facecolor of the axes (space in b/w the axes) should be a little different to contrast
  the image with the background.

## Code
```python
fig = plt.figure(facecolor=(.27,.27,.3))
plt.style.use('dark_background')

# ...

ax = plt.subplot()
ax.set_facecolor((.44, .45, .45))

# ...

plt.show()
```

## Learn More
1. ["Adding multiple attributes with Kramdown"](https://www.stevefenton.co.uk/blog/2022/09/adding-multiple-attributes-with-kramdown/) 
by Steve Fenton.
2. Markdown renderer supported by Jekyll - [Kramdown](https://jekyllrb.com/docs/configuration/markdown/#kramdown).
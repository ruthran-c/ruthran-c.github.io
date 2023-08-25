---
title: View Jekyll drafts and future posts
date: 2023-08-25 00:05:00 +0530
categories: [Snippets, Recall]
tags: [jekyll, code]
---

## How to create a Jekyll draft?
All you have to do is simply create a directory called `_drafts`{: .filepath} in the
site's root and place your draft posts inside.

> Avoid including a date in the **file name** and the **front matter** for draft posts.
{: .prompt-warning }

## Build Jekyll site locally
To build the Jekyll site locally, one of the two below commands can be used.
1. `jekyll serve`
2. `bundle exec jekyll serve`

depending on whether you use Jekyll through [Bundler](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/) or have it installed
directly to the system.

## View drafts and future content
1. Using the `--drafts` flag with the terminal command will allow Jekyll to
read the source files under `_drafts`{: .filepath} and build your site.
2. Using the `--future` flag with the terminal command will allow you to view
all posts that are dated in the future.
3. Without the `--future` flag, all source files dated in the future will be skipped 
over including those under `_drafts`{: .filepath}
 - System message &rarr; `Skipping: _drafts/2023-09-25-test.md has a future date`{: .filepath}
   {: .prompt-info }

## Code
My current `serve` command looks like this:
```zsh
bundle exec jekyll s --port 4002 --drafts --future
```
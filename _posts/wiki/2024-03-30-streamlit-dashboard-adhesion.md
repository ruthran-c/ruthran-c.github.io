---
title: Dashboard using Streamlit
date: 2024-03-30 23:20:00 -0500
categories: [Wiki]
tags: [tableau, dataviz, streamlit, python, dashboard, html-embed]
---
Streamlit is a Python library used to convert pure python scripts into web apps. This is an exploration of Streamlit's
capabilities to build a dashboard.

## Plan
1. Build a dashboard with at least one visualization and KPIs.
2. Have a tab to view the dataset.
3. Create a universal filter within the app to dynamically adjust all elements of the dashboard.
4. Embed external visualizations from tools such as Tableau.

## Project structure
The project's file structure is very similar to any other python project. Other than the main `app.py` file,
the directory contains 2 folders, `./data` and `./proc` - The data and custom package directories for the app.

The `proc` package consists of 2 modules, `./proc/core.py` and `./proc/const.py`. The **core** module contains 
most of the functions, data import and data cleaning and EDA. The **const** module contains the global constants.

```
.
|- README.md
|- data/
|   |-
|- proc/
|   |-
|- app.py
|- jupyter-notebook.ipynb
|- other/
|   |-
```

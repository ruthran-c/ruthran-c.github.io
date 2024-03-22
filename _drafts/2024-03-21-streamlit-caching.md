---
title: Caching with Streamlit
date: 2024-03-21 09:45:00 -0500
categories: [Wiki]
tags: [python]
---

Streamlit runs your script from top to bottom at every user interaction or code change.[^caching]

## Hashing
```python
@st.cache_data
def load_data(url):
    df = pd.read_csv(url)
    return df
```
{% include sample.html %}

## Resources
[^caching]:[Streamlit - Caching](https://docs.streamlit.io/library/advanced-features/caching)
[^state]:[Streamlit - Add statefulness to apps](https://docs.streamlit.io/library/advanced-features/session-state)
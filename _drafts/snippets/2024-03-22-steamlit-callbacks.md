---
title: Streamlit Callbacks with Session State
date: 2024-03-22 22:55:00 -0500
categories: [Snippets, Streamlit]
tags: [streamlit, python]
---

> As a data scientist, targeted analysis through filters for your 
models and visualizations is standard practise. This allows stakeholders to 
explore your findings from different perspectives.
{: .prompt-info}

Let's say you want to build a dashboard for clients. This dynamic 
dashboard needs to be interactive based on user input. You factor in the need for filters and build 
it into your Streamlit app.

```python
# Filter data to within [amount-500, amount+500] range.
# We only want to look at the $1000 range around chosen 'amount'.
import streamlit as st
amount = st.number_input(label="Amount",
                         max_value=9500,
                         key='amount'
                         )
st.session_state.amount = (amount-500, amount+500)
st.dataframe(df[(df.amount>st.session_state.amount[0])&
                (df.amount<st.session_state.amount[1])])
```
This will not 
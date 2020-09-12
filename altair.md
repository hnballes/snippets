# Overview

## Bar Chart

```python
trend_bar = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="value",
    color="search_term"
)
```

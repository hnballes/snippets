# Overview

## Bar Chart

```python
trend_bar = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="value",
    color="search_term"
)
```

##line Chart
```python
trend_line = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y="mean(value)",
    color="search_term"
)
```

##Scatter Chart
```python
scatter_brain_body = alt.Chart(brain).mark_circle().encode(
    x='Body Weight',
    y='Brain Weight'
).properties(
    width=700,
    height=300,
    title="Relación peso del cerebro y del cuerpo"
).interactive()
```

##Histograma
```python
# Histogram
alt.Chart(brain).mark_bar().encode(
    x=alt.X('Brain Weight',bin=True),
    y="count()"
)
```

##MAP
##puntos en el mapa
```python
points = alt.Chart(temp).mark_circle().encode(
    latitude="lat",
    longitude="lon",
    color=alt.Color("mean(temp)",scale=alt.Scale(domain=[-30,10,40],range=["lightblue","orange","red"]))
)
```
##dibujar el mapa de fondo
##remote geojson data object
```python
url = "https://raw.githubusercontent.com/datasets/geo-countries/master/data/countries.geojson"
data_geojson_remote = alt.Data(url=url, format=alt.DataFormat(property='features',type='json'))
```
##chart object
```python
background = alt.Chart(data_geojson_remote).mark_geoshape(
    fill="lightgrey",
    stroke="white"
).encode(
).properties(
    
)

(background+points)
```
# Composiciones
```python
scatter_snake|bar_snake
```
```python
mini_trend_line&trend_line
```
# selecciones
```python
select_date = alt.selection(type="interval",encodings=["x"])

mini_trend_line = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y="mean(value)",
    color="search_term"
).properties(
    height=100
).add_selection(
    select_date
)

trend_line = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y="mean(value)",
    color="search_term"
).transform_filter(
    select_date
)
```

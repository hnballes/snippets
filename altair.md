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
# cambiar configuracion del tema

```python
config = {'arc': {'fill': '#30a2da'},
 'area': {'fill': 'black'},
 'axisBand': {'grid': False},
 'axisBottom': {'domain': False,
  'domainColor': '#999',
  'domainWidth': 3,
  'grid': False,
  'gridColor': '#cbcbcb',
  'gridWidth': 1,
  'labelColor': '#999',
  'labelFontSize': 14,
  'labelPadding': 4,
  'tickColor': 'white',
  'tickSize': 10,
  'titleFontSize': 14,
  'titlePadding': 10},
 'axisLeft': {'domainColor': 'white',
  'domainWidth': 1,
  'grid': False,
  'gridColor': 'white',
  'gridWidth': 1,
  'labelColor': 'white',
  'labelFontSize': 10,
  'labelPadding': 4,
  'tickColor': 'white',
  'tickSize': 10,
  'ticks': True,
  'titleFontSize': 14,
  'titlePadding': 10},
 'axisRight': {'domainColor': '#333',
  'domainWidth': 1,
  'grid': True,
  'gridColor': '#cbcbcb',
  'gridWidth': 1,
  'labelColor': 'white',
  'labelFontSize': 10,
  'labelPadding': 4,
  'tickColor': 'white',
  'tickSize': 10,
  'ticks': True,
  'titleFontSize': 14,
  'titlePadding': 10},
 'axisTop': {'domain': False,
  'domainColor': '#333',
  'domainWidth': 3,
  'grid': False,
  'gridColor': '#cbcbcb',
  'gridWidth': 1,
  'labelColor': '#999',
  'labelFontSize': 10,
  'labelPadding': 4,
  'tickColor': '#cbcbcb',
  'tickSize': 10,
  'titleFontSize': 14,
  'titlePadding': 10},
 'background': 'white',
 'group': {'fill': 'black',"stroke":"white"},
 'legend': {'labelColor': '#333',
  'labelFontSize': 14,
  'padding': 1,
  'symbolSize': 30,
  'symbolType': 'square',
  'titleColor': '#333',
  'titleFontSize': 14,
  'titlePadding': 10},
 'line': {'stroke': '#30a2da', 'strokeWidth': 2},
 'path': {'stroke': '#30a2da', 'strokeWidth': 0.5},
 'rect': {'fill': '#30a2da'},
 'range': {'category': ['#30a2da',
   '#fc4f30',
   '#e5ae38',
   '#6d904f',
   '#8b8b8b',
   '#b96db8',
   '#ff9e27',
   '#56cc60',
   '#52d2ca',
   '#52689e',
   '#545454',
   '#9fe4f8'],
  'diverging': ['#cc0020',
   '#e77866',
   '#f6e7e1',
   '#d6e8ed',
   '#91bfd9',
   '#1d78b5'],
  'heatmap': ['#d6e8ed', '#cee0e5', '#91bfd9', '#549cc6', '#1d78b5']},
 'symbol': {'filled': True, 'shape': 'circle'},
 'shape': {'stroke': 'white'},
 'style': {'bar': {'binSpacing': 2, 'fill': '#30a2da', 'stroke': None}},
 'title': {'anchor': 'start', 'fontSize': 24, 'fontWeight': 600, 'offset': 20},
         "view": {
     "stroke": "transparent"
  }}
```
```python
def my_theme():
    return {'config': config }

alt.themes.register('my_theme', my_theme)

alt.themes.enable('my_theme')
```

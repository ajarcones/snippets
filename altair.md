

# altair CHARTS

## Import altair

```python
import altair as alt
# if in notebook
alt.renderers.enable("notebook")
```

# HISTOGRAM CHART
```python
alt.Chart(df).mark_bar().encode(
    x=alt.X('Brain Weight', bin=True, title="Brain Weight Binned"),
    y="count()"
).properties(
    width=200,
    height=200,
    title="Histogram of Brain Weight"
)
```

# SCATTER CHART
```python
scatter_plt = alt.Chart(df).mark_circle().encode(
    x="Body Weight",
    y="Brain Weight"
) title="Histogram of Brain Weight"
```

# BAR CHART
```python
trends_bar_chart=alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="sum(value)",
    color="search_term"
)
```

# LINE CHART
```python
trends_line_chart=alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
)
```
# HORIZONTAL CONCATENATION
```python
trends_bar_chart|trends_line_chart
```

# VERTICAL CONCATENATION
```python
trends_line_chart&trends_line_chart_small
```

# CHART INTERACTION

# SINGLE SELECTION
```python
# CLICK EN BARRRA MUESTRA SOLO CURVA DE ESA BARRA (LINEA)
select_search_term = alt.selection_single(encodings=["x"])

trends_line_chart=alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
).transform_filter(
        select_search_term.ref()
)

trends_bar_chart=alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="sum(value)",
    color="search_term"
).properties(
    selection = select_search_term
)
```

# INTERVAL SELECTION WITH ZOOM
```python
# HACER UNA SELECCION DE INTERVALO EN LINE CHART MAS PEQUEÑO (QUE SEA ZOOM EL INICIAL)
# PARA QUE SE MUESTRE EN EL LINE CHART INICIAL LA CURVA CORRESPONDIENTE SOLO AL
# INTERVALO SELECCIONADO.
# ASI CONSEGUIMOS UN EFECTO ZOOM SOBRE INTERVALOS DEL LINE CHART INICIAL
select_interval = alt.selection_interval(encodings=["x"])

trends_line_chart=alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
).transform_filter(
    select_interval
)

trends_line_chart_small=alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="sum(value)",
    color="search_term"
).properties(
    height=50,
    selection = select_interval
)
```

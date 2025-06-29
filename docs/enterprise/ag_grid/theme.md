---
order: 3
---


# Themes

```python
import reflex as rx
```

```python
rx.callout(
    "Only the old theme API of AG Grid is currently supported. The new theme API is not supported yet.",
    icon="triangle_alert",
    color_scheme="orange",
    size="1",
)
```

You can style your grid with a theme. AG Grid includes the following themes:

1. `quartz`
2. `alpine`
3. `balham`
4. `material`

The grid uses `quartz` by default. To use any other theme, set it using the `theme` prop, i.e. `theme="alpine"`.

```python
import reflex as rx
import reflex_enterprise as rxe
import pandas as pd

class AGGridThemeState(rx.State):
    """The app state."""

    theme: str = "quartz"
    themes: list[str] = ["quartz", "balham", "alpine", "material"]

df = pd.read_csv("https://raw.githubusercontent.com/plotly/datasets/master/gapminder2007.csv")

column_defs = [
    dict(field="country"),
    dict(field="pop", headerName="Population"),
    dict(field="lifeExp", headerName="Life Expectancy"),
]

def ag_grid_simple_themes():
    return rx.vstack(
        rx.hstack(
            rx.text("Theme:"),
            rx.select(AGGridThemeState.themes, value=AGGridThemeState.theme, on_change=AGGridThemeState.set_theme),
        ),
        rxe.ag_grid(
            id="ag_grid_basic_themes",
            row_data=df.to_dict("records"),
            column_defs=column_defs,
            theme=AGGridThemeState.theme,
            width="100%",
            height="40vh",
        ),
        width="100%",
    )
```

[Home Page](/)
[AG Grid](/docs/enterprise/ag-grid/)

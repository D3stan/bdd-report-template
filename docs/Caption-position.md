The **`.captionposition`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Document/captionposition.html)</sup> function allows globally setting the position of captions, relative to the element they describe.

This applies to:
- Figures
  - [Figure Markdown extension](https://github.com/iamgio/quarkdown/wiki/figure)
  - [`.figure`](https://github.com/iamgio/quarkdown/wiki/custom-figure)
  - [Mermaid diagrams](https://github.com/iamgio/quarkdown/wiki/mermaid-diagrams) and derivatives (e.g. [XY charts](https://github.com/iamgio/quarkdown/wiki/xy-chart))
- Tables
  - [Table caption Markdown extension](https://github.com/iamgio/quarkdown/wiki/table-caption)
  - [Tables from CSV](https://github.com/iamgio/quarkdown/wiki/File-data#table-from-csv)

---

The function's primary parameter is called `default`, which sets the global style for all kinds of captioned elements.  
Additional parameters `figures` and `tables` override the default position for those specific categories.

Each parameter is optional and accepts `top`/`bottom` values.  
By default, documents use `.captionposition {bottom}`.

&nbsp;

```markdown
.captionposition {bottom}

![Sky](sky.jpg "A nice sky.")

| Name | Favorite food | Favorite beverage |
|------|---------------|-------------------|
| John | Chicken       | Orange juice      |
| Jane | Pasta         | Iced tea          |
| Joe  | Sushi         | Beer              |
"Survey results."
```
<img width="600" alt="Default: bottom" src="https://github.com/user-attachments/assets/a77154fd-d601-4f9c-b469-42055be10c16" />

&nbsp;

```
.captionposition {top}
```
<img width="600" alt="Default: top" src="https://github.com/user-attachments/assets/6ba066d3-53a4-4c4e-a78c-eb305f244350" />

&nbsp;

```
.captionposition {bottom} tables:{bottom}
```
<img width="600" alt="Default: bottom, tables: top" src="https://github.com/user-attachments/assets/0838ac08-08aa-4479-b915-fc0c31df2e59" />


&nbsp;

&nbsp;

> Photo credits: [Pixabay](https://www.pexels.com/photo/blue-skies-53594/)
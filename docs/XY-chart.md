The **`.xychart`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Mermaid/xychart.html)</sup> function allows plotting 2D line/bar charts in a pure, flexible Quarkdown fashion, through the power of [Mermaid](mermaid-diagrams).

All its parameters, except for `values`, are optional.

| Parameter   | Description                                                                | Accepts                 |
|-------------|----------------------------------------------------------------------------|-------------------------|
| `lines`     | Whether to draw lines (defaults to true).                                  | [Boolean](boolean)      |
| `bars`      | Whether to draw bars (defaults to false).                                  | [Boolean](boolean)      |
| `x`         | Label for the X axis.                                                      | String                  |
| `xrange`    | Numerical range for the X axis. Can be open-ended. Incompatible with `xtags`. | [Range](range) |
| `xtags`     | Categorical tags for the X axis. Incompatible with `xrange`.               | [Iterable](iterable)    |
| `y`         | Label for the Y axis.                                                      | String                  |
| `yrange`    | Range for the Y axis. Can be open-ended.                                   | [Range](range)          |
| `caption`   | Caption. If present, the chart is [numbered](numbering) as a figure.       | String                  |
| `values`    | Y values to plot. | <ul><li>[Iterable](iterable) of points (single line)</li><li>Iterable of iterables of points (multiple lines)</li></ul> |

### Axis ranges

`xrange` and `yrange` define the boundaries of the visible area of the chart, through the usual `x..y` [Range](range) syntax.

The range may also be open on either end, or both.
- If open on the left end, the range starts from the minimum value among the plotted points.
- If open on the right end, the range ends at the maximum value among the plotted points.

For instance, `..` (infinite) is the default range, which shows the area between the minimum and maximum values.

&nbsp;

# Possible input sources

## From static list

`values` can be represented by a Markdown list, just like all iterables.

```
.xychart bars:{yes} x:{Months} y:{Revenue} yrange:{100..}
  - 250
  - 500
  - 350
  - 450
  - 400
  - 500
  - 600
```

<img width="600" alt="Simple list" src="https://github.com/user-attachments/assets/8521d32f-fb23-491c-956c-07615e53807a" />

&nbsp;

In case of nested lists (iterable of iterables), multiple lines will be plotted:

```
.xychart x:{Months} y:{Revenue}
  - - 250
    - 500
    - 350
    - 450
    - 400

  - - 400
    - 150
    - 200
    - 400
    - 450
```

<img width="600" alt="Nested lists" src="https://github.com/user-attachments/assets/6c92df85-f98e-480e-9740-6a1b32298530" />

&nbsp;

## From CSV/table

[Table manipulation](table-manipulation) functions such as [`.tablecolumn`](table-manipulation#retrieve-columns) can extract values from the columns of a table as iterables.

```
.xychart
    .tablecolumn {2}
        .csv {data.csv}
```

In case multiple columns must be accessed from the same table, consider calling `.tablecolumns`, which returns a collection of columns, for efficiency.
Any [`Iterable`](iterable) operation can then be performed.

In the following example, the chart displays two lines: one for the second and one for the third column of the CSV.
Additionally, the first column of the table is used as a set of categorical tags for the X axis.

```
.var {columns}
    .tablecolumns
        .csv {data.csv}

.xychart xtags:{.columns::first} x:{Years} y:{Sales}
    .columns::second
    .columns::third
```

<img width="600" alt="CSV" src="https://github.com/user-attachments/assets/dddae1c0-cded-483a-9c84-8b59096d1880" />

&nbsp;

## From iterations

Quarkdown [loops](loops) return an iterable containing the result of each iteration, making them a suitable input for `values`, especially in combination with [math](math) functions.

```
.xychart
    .repeat {100}
        .1::pow {2}::divide {100}
    
    .repeat {100}
        .1::logn::multiply {10}
```

<img width="600" alt="Loop" src="https://github.com/user-attachments/assets/c27f6f8f-fb38-4d97-81ac-46da19b719e3" />
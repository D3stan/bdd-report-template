The following table operations can affect not only plain Markdown tables, but also any kind of table including those [loaded from CSV](file-data#table-from-csv).

<details>
<summary>CSV example</summary>

```
.tablesort {2} order:{descending}
    .csv {people.csv}
```

</details>

# Sort rows

The **`.tablesort`** function sorts a table based on the values of a specific column.

| Parameter | Description | Accepts |
|-----------|-------------|---------|
| `column` | Index of the column, starting from 1. | 1 to number of columns. |
| `order` | Sorting order. | `ascending` (default), `descending` |

```
.tablesort {2} order:{descending}
    | Name | Age | City |
    |------|-----|------|
    | John | 25  | NY   |
    | Lisa | 32  | LA   |
    | Mike | 19  | CHI  |
```
> Result:
> ```
> | Name | Age | City |
> |------|-----|------|
> | Lisa | 32  | LA   |
> | John | 25  | NY   |
> | Mike | 19  | CHI  |
> ```

&nbsp;

# Filter rows

The **`.tablefilter`** function keeps or removes rows based on the values of a specific column.

| Parameter | Description | Accepts |
|-----------|-------------|---------|
| `column` | Index of the column, starting from 1. | 1 to number of columns. |
| `filter` | Lambda that returns whether each row should be kept, with the value of its cell in the corresponding column as input. | [`Dynamic`](typing)→[`Boolean`](boolean) [lambda](lambda) |

```
.tablefilter {2} {@lambda x: .x::isgreater {20}}
    | Name | Age | City |
    |------|-----|------|
    | John | 25  | NY   |
    | Lisa | 32  | LA   |
    | Mike | 19  | CHI  |
```
> Result:
> ```
> | Name | Age | City |
> |------|-----|------|
> | John | 25  | NY   |
> | Lisa | 32  | LA   |
> ```

&nbsp;

# Compute/aggregate columns

The **`.tablecompute`** function computes the cells in a column and appends the result to a new row.

| Parameter | Description | Accepts |
|-----------|-------------|---------|
| `column` | Index of the column, starting from 1. | 1 to number of columns. |
| `compute` | Lambda that returns the computed value, with the collection of the cells in the column as input. | [`Iterable`](iterable)→[`Dynamic`](typing) [lambda](lambda) |

See [*Iterable*](iterable) to learn more about available operations on collections.

**Example**:
```markdown
.tablecompute {2} {@lambda x: .x::average::round}
    | Name | Age | City |
    |------|-----|------|
    | John | 25  | NY   |
    | Lisa | 32  | LA   |
    | Mike | 19  | CHI  |
```
> Result:
> ```
> | Name | Age | City |
> |------|-----|------|
> | John | 25  | NY   |
> | Lisa | 32  | LA   |
> | Mike | 19  | CHI  |
> |      | 25  |      |
> ```

&nbsp;

# Composition

Multiple table operations can be chained. The order of the operations goes from inner to outer:

```
.tablecompute {2} {@lambda x: .x::average::round}
    .tablesort {2}
        | Name | Age | City |
        |------|-----|------|
        | John | 25  | NY   |
        | Lisa | 32  | LA   |
        | Mike | 19  | CHI  |
```
> Result:
> ```
> | Name | Age | City |
> |------|-----|------|
> | Mike | 19  | CHI  |
> | John | 25  | NY   |
> | Lisa | 32  | LA   |
> |      | 25  |      |
> ```

&nbsp;

# Retrieve columns

The **`.tablecolumn`** function extracts values from the cells of a specific column, and returns them as an [Iterable](iterable).

| Parameter | Description | Accepts |
|-----------|-------------|---------|
| `column` | Index of the column, starting from 1. | 1 to number of columns. |

```
.var {values}
    .tablecolumn {2}
        | Name | Age | City |
        |------|-----|------|
        | John | 25  | NY   |
        | Lisa | 32  | LA   |
        | Mike | 19  | CHI  |

.values::first
```
> Result: `25`

&nbsp;

Additionally, the **`.tablecolumns`** function returns all the columns from the table, as an iterable of iterables.
This is more efficient in case you need to access multiple columns from the same table.

```
.var {columns}
    .tablecolumn
        | Name | Age | City |
        |------|-----|------|
        | John | 25  | NY   |
        | Lisa | 32  | LA   |
        | Mike | 19  | CHI  |

.foreach {.columns}
  col:
  .col::first
```
> Result:
> ```
> John
> 25
> NY
> ```
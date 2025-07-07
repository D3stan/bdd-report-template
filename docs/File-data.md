Quarkdown offers functions to retrieve information from files.

> [!NOTE]
> The following functions refer to a `path` parameter, which accepts the path to the target file, which may be relative to the location of the main source file, or absolute.  
> A slash (`/`) is the global path separator, agnostic to the current file system in use.

# File text content

The **`.read {path}`** function returns the string content of the given file.

An optional `lines` parameter of type [`Range`](range) is also supported, which allows for the selection of a specific range of lines (inclusive, starting from 1). An invalid or out of bounds range causes an error.  
If no range is provided, the whole file is read.

```
.read {myfile.txt} lines:{3..8}
```

The strategy used for open ranges is defined as follows:

- If the range is open on the left end (`..N`) it starts reading from the beginning of the file until line `N`.
- If the range is open on the right end (`N..`) it reads from line `N` to the end of the file.
- If the range is open on both ends (`..`) the whole file is read.

> [!TIP]
> `.read` can be particularly useful when used in combination with [`.code`](code) and [`.mermaid`](mermaid-diagrams) in order to load code snippets from external files:
>
> ```
> .code {java}
>   .read {Point.java}
> ```

# Table from CSV

The **`.csv {path}`** function loads a table from a CSV file.
The first row of the CSV file is always used as the header row.

```
.csv {people.csv}
```

A caption can also be provided:

```
.csv {people.csv} caption:{People data.}
```

Tables loaded from CSV can also be manipulated: see [*Table manipulation*](table-manipulation) for more.
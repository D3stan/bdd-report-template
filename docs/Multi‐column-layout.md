[**`.pageformat {columns}`**](page-format) applies a multi-column layout to each page, given that the value of `columns` is higher than 1.

<img width="700" alt="Example" src="https://github.com/user-attachments/assets/0f844b46-ac01-4245-87ae-4fc85506f9ab">

> `.pageformat columns:{2}`

> [!CAUTION]
> Multi-layout column is yet unstable in `paged` documents and is inconsistent across browsers (specially Safari).  
> If you know how to improve the result via Paged.js, please open a PR.

# Span property

When in a multi-column layout all elements, except for level 1-3 headings, are rendered within their own column.  
It's possible to set some content to instead span across all columns of the layout by using the **`.fullspan`** block function.

```
...

.fullspan
  ![](img.png)

...
```

To do: example
Blank space can be added anywhere via the **`.whitespace`** function, which accepts optional `width` and `height` [Size](sizes#single-size-size) arguments.

- If none is set, a simple whitespace character is rendered (`&nbsp;`), useful to add blank lines.
- If at least one is set, a rectangle of that size is rendered. This might not always work if it's outside of [layout functions](stack-layout-functions).

```html
Line 1

.whitespace <!-- A larger line break -->

Line 2
```

```
.row
  A

  .whitespace width:{2px}

  B
```
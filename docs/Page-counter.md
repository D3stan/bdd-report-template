The **`.currentpage`** and **`.totalpages`** functions display, respectively, the current index (beginning from 1) of the page/slide the function call lies in and the total amount of pages/slides. They don't accept any argument.

They are unsupported in `plain` documents, where the `-` placeholder is shown instead.

> [!NOTE]
> These functions return visual elements (nodes), *not* numbers. Hence, it is not allowed to do, for example, `.sum {.currentpage} {3}`.

# Fixed page counter

A page counter can be displayed on each page thanks to [page margin content](page-margin-content):

```
.pagemargin {bottomcenter}
  .currentpage / .totalpages
```
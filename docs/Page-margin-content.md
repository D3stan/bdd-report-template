The **`.pagemargin`** function displays content on each page, in a fixed position along its [margins](page-format#content-area).

- In `paged` documents, a special area of each page is reserved for margins:  

  <img height="500" alt="Paged margin areas" src="https://github.com/user-attachments/assets/bc41b306-df24-4753-960e-486953f1adb2">
  
  > Credits: [Paged.js](https://pagedjs.org/documentation/7-generated-content-in-margin-boxes/#margin-boxes-of-a-page)

- In `plain` and `slides` documents, content set on margins could potentially overlap page content.

- In `plain` documents, where the concept of *page* does not exist, page margins are displayed once per document.

The function accepts an optional `position` and a body argument `content`:

| Parameter | Description | Accepts |
|-----------|-------------|---------|
| `position` | Page area to target. | `topleftcorner`, `topleft`, `topcenter` (default), `topright`, `toprightcorner`, `righttop`, `rightmiddle`, `rightbottom`, `bottomrightcorner`, `bottomright`, `bottomcenter`, `bottomleft`, `bottomleftcorner`, `leftbottom`, `leftmiddle`, `lefttop` |
| `content` | Element to display. | [Block content](markdown-content#block-content) |

```
.pagemargin {topright}
  **This** is a margin content.
```

<img width="500" alt="Page margin" src="https://github.com/user-attachments/assets/ef0dfc4d-14b7-4def-a2f8-44f4c6b55d67" />


# Footer

Most layout themes associate the `bottomcenter` margin to the document footer, and style it differently - for instance, different blocks may be displayed in a row. Footers are particularly used in `slides` documents.

The **`.footer`** function is a shorthand for `.pagemargin {bottomcenter}`.

```
.theme {beaver} layout:{beamer}

.footer
  .docauthor

  **.docname**

  [GitHub](https://github.com/iamgio/quarkdown)
```

<img width="700" alt="Page footer" src="https://github.com/user-attachments/assets/2fd57bef-e6ed-48b4-a7b6-dd71a03030cd" />


# Page counter

A page margin can host a page counter: see [Page counter](page-counter).
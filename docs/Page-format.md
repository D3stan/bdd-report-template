The **`.pageformat`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Document/pageformat.html)</sup> function configures the page format. All its parameters are **optional** and if unset will delegate their default value to the underlying renderer depending on the document type.

| Parameter | Description | Accepts | Supported documents |
|-----------|-------------|---------|-------------------------|
| `size` | Name of the paper format. | `A0`..`A10`, `B0`..`B5`, `letter`, `legal`, `ledger` | `paged`, `slides` |
| `width` | Page width. If `size` is set too, this value overrides its width. | [`Size`](sizes#size-single-size), e.g. `300px`, `15cm`, `5.8in` | `paged`, `slides` |
| `height` | Page height. If `size` is set too, this value overrides its height. | [`Size`](sizes#size-single-size), e.g. `300px`, `15cm`, `5.8in` | `paged`, `slides` |
| `orientation` | Whether width and height of the paper format (`size`) should be swapped. This defaults to `portrait` for `plain` and `paged` documents and to `landscape` for `slides`. | `portrait`, `landscape` | `paged`, `slides` |
| `margin` | Blank space between page borders and [content area](content-area). | [`Sizes`](sizes#size-group-sizes), e.g. `1cm`, `15mm 30px`, `2in 1in 3in 2in` | `plain`, `paged`, `slides` |
| `bordertop`, `borderright`, `borderbottom`, `borderleft` | Thickness of the border at each side of the [content area](content-area). | [`Size`](sizes) | `paged`, `slides` |
| `bordercolor` | Color of the border around the [content area](content-area). | [`Color`](color) | `paged`, `slides` |
| `columns` | Number of columns in each page.<br>If set to 2 or higher, the document has a [multi-column layout](multi%E2%80%90column-layout). | Positive integer | `plain`, `paged`, `slides` |
| `alignment` | Horizontal content and text alignment. | `start` (default in `slides`), `center`, `end`, `justify` (default in `plain` and `paged`) | `plain`, `paged`, `slides` |

&nbsp;

# Content area

Each page is composed of a *content area* in which the main content is displayed, and a *margin area*, a blank outline that may host [page margin content](page-margin-content) such as [page counters](page-counter).

<img width="400" alt="Content area" src="https://github.com/user-attachments/assets/aef08bca-e097-4822-8b16-2bb41f480f06">

&nbsp;

## Margins

The `margin` parameter affects the size of the margin area, thus reducing the surface of the content area.

```
.pageformat margin:{4cm}
```

<img width="400" alt="Margins" src="https://github.com/user-attachments/assets/01acf7a0-dfe8-4a74-bcaf-4df64351477b">

&nbsp;

## Borders

`bordertop`, `borderright`, `borderbottom`, `borderleft` and `bordercolor` allow customization of borders around the content area of each page in `paged` and `slides` documents.
- If at least one side is specified, the border will apply to the specified sides. If the color is not specified it will use the default foreground text color;
- If no side is specified, but the color is, the border will apply to all sides with a default thickness.

```
.pageformat bordertop:{1px} borderbottom:{4px}
```

<img width="400" alt="image" src="https://github.com/user-attachments/assets/639fec14-3c6b-4bf8-9b80-6c8cad620b1b" />

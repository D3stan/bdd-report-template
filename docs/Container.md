The **`.container`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Layout/container.html)</sup> function generates a highly customizable blocks of content, along with resetting the current layout rules back to normal.

---

Image you want to make a row with two columns, each one with a heading and some text below. The following is what a novice might attempt:

```html
<!-- WRONG! -->
.row alignment:{center} gap:{1cm}
  ## Left
  Text on left column.
    
  ## Right
  Text on right column.
```

As mentioned in the [Stacks](stacks) page:

> In order to understand which elements they *[stack functions]* must handle, they rely on the strict Markdown concept of block, an isolated chunk of the document [...]

Rendering the previous snippet brings us to this (incorrect) result:

<img width="556" alt="Incorrect result" src="https://github.com/user-attachments/assets/86da7885-aa0f-4ba5-a4ef-adae47d445cb">

Some may then use columns:

```html
<!-- Could be improved -->
.row alignment:{center} gap:{1cm}
  .column cross:{start}
    ## Left
    Text on left column.
    
  .column cross:{start}
    ## Right
    Text on right column.
```

This works, but the concept isn't really correct: we don't want some *layout rule*, we just want to reset the document flow back to normal.  
This is what the container layout does: grouping elements together according to the natural flow of the document.

```html
<!-- Correct! -->
.row alignment:{center} gap:{1cm}
  .container
    ## Left
    Text on left column.
    
  .container
    ## Right
    Text on right column.
```

Result:

<img width="556" alt="Correct result" src="https://github.com/user-attachments/assets/c97db6c3-c311-4177-a0be-6c1608dab86e">

# Styling

Optional parameters:

| Parameter | Description | Accepts | Default |
|-----------|-------------|---------|---------|
| `width` | Box width constraint. | [`Size`](sizes) | No constraint. |
| `height` | Box height constraint. | [`Size`](sizes) | No constraint. |
| `fullwidth` | Whether to take up the parent's full width.<br>Overridden by `width`. | [`Boolean`](boolean) | False |
| `foreground` | Text color. | [`Color`](color) | Document's default. |
| `background` | Background color. | [`Color`](color) | (none) |
| `border` | Border color. | [`Color`](color) | Browser's default if `borderwidth` is set, none otherwise. |
| `borderwidth` | Border size. | [`Sizes`](sizes) | Browser's default if `border` is set, none otherwise. |
| `borderstyle` | Border type. | `normal`, `dashed`, `dotted`, `double` | `normal` if `border` or `borderwidth` is set, none otherwise. |
| `margin ` | Whitespace outside content. | [`Sizes`](sizes) | (none) |
| `padding ` | Whitespace around content. | [`Sizes`](sizes) | (none) |
| `radius` | Corner/border radius. | [`Sizes`](sizes) | (none) |
| `alignment` | Content alignment. | `start`, `center`, `end` | Browser's default. |
| `textalignment` | Text alignment. | `start`, `center`, `end`, `justify` | Browser's default. |
Whereas base Markdown requires HTML code to constrain the size of an image, Quarkdown introduces a new syntax extension to achieve the same result in a more elegant and efficient way:

```markdown
!(200x150)[Alt](image.png)

<!-- or -->

!(200*150)[Alt](image.png)

<!-- or -->

!(200 150)[Alt](image.png)
```

The previous (equivalent) examples load `image.png` with the label `Alt` as CommonMark Markdown would do, but also adding an additional size constraint, making the visible image fit into a 200px by 150px box.

Apart from pixels, whose unit can be omitted, any other [size](sizes) unit is supported. In this case the `x` delimiter can no longer be used, in favor of either `*` or a space.

```markdown
!(5cm*35mm)[Alt](image.png)

<!-- or -->

!(2.5in 1cm)[Alt](image.png)

<!-- but not this -->

!(2.5inx1cm)[Alt](image.png)

<!-- '%' is an exception. This is valid (although not so readable) -->

!(30%x150%)[Alt](image.png)
```

In case one of the components (width or height) is equal to `_` (underscore), it becomes automatic, meaning that component is automatically calculated in order to keep the original aspect ratio.

- Auto height examples:
  ```markdown
  <!-- 300px width, auto height -->
  !(300x_)[Alt](image.png)

  <!-- 5cm width, auto height -->
  !(5cm*_)[Alt](image.png)

  <!-- 2in width, auto height -->
  !(2in _)[Alt](image.png)

  <!-- 50% width, auto height -->
  !(50% _)[Alt](image.png)
  ```

  Additionally, as a convenient shorthand, automatic height can be omitted:
  ```markdown
  <!-- 300px width, auto height -->
  !(300)[Alt](image.png)

  <!-- 5cm width, auto height -->
  !(5cm)[Alt](image.png)

  <!-- 2in width, auto height -->
  !(2in)[Alt](image.png)

  <!-- 50% width, auto height -->
  !(50%)[Alt](image.png)
  ```

- Auto width examples:
  ```markdown
  <!-- auto width, 100px height -->
  !(_x100)[Alt](image.png)

  <!-- auto width, 15mm height -->
  !(_*15mm)[Alt](image.png)

  <!-- auto width, 2in height -->
  !(_ 2in)[Alt](image.png)
  ```
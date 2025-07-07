A page break is a forced interruption of the page flow, so that content that follows the break will appear on the next page.  
Page breaks do not affect `plain` documents, except for printing.

> [!NOTE]
> The word *page* is exchangeable with *slide* in the context of a `slides` document.

# Manual break

A page break can be triggered by a line containing only a sequence of 3 (or more) `<` characters.  

```
Page 1

<<<

Page 2
```

This pattern does not interrupt the current block, and thus might be seen as plain text if the criteria of closing a block, such as an empty line for paragraphs, are not satisfied. The following example does not trigger a page break:

```
Page 1
<<<
Page 2
```
> Page 1 <<< Page 2

# Automatic break

A heading block (`# This!`) could automatically trigger a page break. 

By default only level-1 headings (one `#` symbol) do, but this can be customized via the **`.autopagebreak`** function, which should conventionally be called in the 'setup' area of the source code (along with metadata, page format, etc.).

This function takes a `maxdepth` integer argument which indicates the maximum level a heading should be in order to trigger a page break. Heading levels range from 1 to 6.

```html
.autopagebreak maxdepth:{3}

# A    <!-- Break -->

## B   <!-- Break -->

### C  <!-- Break -->

#### D <!-- No break -->
```

**`.noautopagebreak`**, which is equivalent to `.autopagebreak {0}`, can be called in order to disable automatic breaks.
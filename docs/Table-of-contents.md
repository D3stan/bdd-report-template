A table of contents is a quick summary of the document, where links to headings are displayed in a visual hierarchy.

- `paged` documents also display the corresponding page number.
- `slides` documents constrain the maximum height, making it vertically scrollable.

A ToC can be displayed through the **`.tableofcontents`** function, with the following optional parameters:

| Parameter | Description | Accepts | Default |
|-----------|-------------|---------|---------|
| `title` | Title that precedes the ToC.<br />If unset, it's automatically localized. | Inline content | Automatically localized if [`.doclang`](document-metadata)'s locale is supported. (e.g. `Table of Contents` for English) |
| `maxdepth` | Maximum level of headings to display.<br />e.g. `maxdepth = 2` collects `# This` and `## This`, but not `### This`. | `Integer` | `3` |
| `focus` | If set, adds focus to the item with the same text as this argument.<br/>Inline style (strong, emphasis, etc.) is ignored when comparing the text content. | [Inline content](markdown-content#inline-content) | (none) |

```
.tableofcontents maxdepth:{2}

# A

...

## A.A

...

## A.B

...

# B

...

# C

## C.A

### C.A.A

...
```

<img width="550" alt="Table of contents" src="https://github.com/user-attachments/assets/87e7b145-0aa1-482e-a66d-3038e7c052ce">

&nbsp;

[Layout themes](theme) greatly influence the look of table of contents:

<img width="550" alt="Table of contents with minimal theme" src="https://github.com/user-attachments/assets/b595ebd0-fafa-4278-b34b-d5da418070ba">

> `minimal` theme

# Ignoring specific headings

[Decorative headings](numbering#decorative-headings) are not numbered and do not appear in table of contents.  
A heading is marked as decorative if a `!` is appended to the last `#` sign. For example `#!`, `##!`, `###!`, etc.

```markdown
##! A decorative heading
```

# Custom numbering

A custom numbering format can be set via `.numbering`. See [Numbering](numbering) for more.

# Focusing & markers

If `focus:{A.B}` is added to the previous example:

<img width="550" alt="Table of contents with focus" src="https://github.com/user-attachments/assets/70bb4947-e7a5-4a6b-9466-d5b53d92ce37">


Focusing may be particularly useful in slides with mini-ToCs at the beginning of each new chapter.  
In that case you may consider defining a function like this:

```
.function {chapter}
    name:
    .tableofcontents maxdepth:{0} focus:{.name}
    .marker {.name}
```

That can be invoked by `.chapter {My chapter}`.

What `.marker` does is creating an invisible level-0 heading (which isn't usually possible with the standard `#`-based heading syntax).  
Setting `maxdepth:{0}` displays only markers in the ToC, ignoring other headings. 
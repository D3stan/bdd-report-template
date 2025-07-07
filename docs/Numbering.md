The **`.numbering`** function sets the global numbering format of the document. When a numbering format is set, counters are displayed in:
- Headings and [table of contents](table-of-contents) entries
- [Figures](figure)
- Tables
- Custom elements (`.numbered`)

The configuration is represented by a [Dictionary](dictionary):

```yaml
.numbering
  - headings: <format>
  - figures: <format>
  - tables: <format>
```

If a key is missing, its numbering is disabled.

Each format parameter accepts either `none` or a string where each character represents either a counter or a fixed symbol:
- `1` for decimal (`1, 2, 3, ...`)
- `a` for lowercase latin alphabet (`a, b, c, ...`)
- `A` for uppercase latin alphabet (`A, B, C, ...`)
- `i` for lowercase roman numerals (`i, ii, iii, ...`)
- `I` for uppercase roman numerals (`I, II, III, ...`)
- Any other character is a fixed symbol

The default numbering format, if unspecified, is:
- For `paged` documents (can be disabled via `.nonumbering`):
  - `1.1.1` for headings;
  - `1.1` for figures and tables.

- None for other documents

# Headings

```markdown
.numbering
  - headings: 1.A.a

# Title    <!--   1   -->
## Title   <!--  1.A  -->
### Title  <!-- 1.A.a -->
### Title  <!-- 1.A.b -->
#### Title <!-- None  -->
## Title   <!--  1.B  -->
# Title    <!--   2   -->
## Title   <!--  2.A  -->
```

<img width="550" alt="Latex theme numbering" src="https://github.com/user-attachments/assets/d6ae1483-43cd-49ea-9934-63c67b8bdd4a">  

<img width="550" alt="Latex theme table of contents" src="https://github.com/user-attachments/assets/1ca513b1-ab48-4d8e-b1f5-46f38e88f75d">

### Decorative headings

To prevent a heading from being numbered, append a `!` after the last `#` sign. For example `#!`, `##!`, `###!`, etc.

```markdown
.center
    #! My document

# Introduction

.loremipsum
```

Decorative headings also don't appear in [table of contents](table-of-contents).

<img width="550" alt="image" src="https://github.com/user-attachments/assets/ac3bfcc2-5a48-4ef3-ad67-7f963357aa3a" />

&nbsp;

# Figures

[Figures](figure) are numbered only if they feature a **caption**, which may also be empty.

```markdown
.numbering
  - headings: 1.A.a
  - figures: 1.1

# Title

![Logo](quarkdown-icon.svg "The Quarkdown icon")

## Title

![Logo](quarkdown-icon.svg "")

# Title

![Logo](quarkdown-icon.svg "")
```

<img width="550" alt="Figure numbering with format 1.1" src="https://github.com/user-attachments/assets/341b6c44-36dd-4304-8a43-3165436531b8">

&nbsp;

When numbering figures and tables, the amount of symbols in the format dictates the rules which cause the counters to reset.  
The previous example, run with `figures:{1}`, results in the following:

<img width="550" alt="Figure numbering with format 1" src="https://github.com/user-attachments/assets/a79104ac-0106-46aa-a7a8-f38f8065b997">


# Tables

Tables are numbered only if they feature a [**caption**](table-caption), which may also be empty.

```markdown
.numbering
  - headings: 1.A.a
  - tables: 1.1

# Title

|           | Age | Favorite food |
|-----------|-----|---------------|
| **Anne**  | 24  | Hamburger     |
| **Lucas** | 19  | Pizza         |
| **Joe**   | 32  | Sushi         |
"Study results."

## Title

|           | Age | Favorite food |
|-----------|-----|---------------|
| **Anne**  | 24  | Hamburger     |
| **Lucas** | 19  | Pizza         |
| **Joe**   | 32  | Sushi         |
""

# Title

|           | Age | Favorite food |
|-----------|-----|---------------|
| **Anne**  | 24  | Hamburger     |
| **Lucas** | 19  | Pizza         |
| **Joe**   | 32  | Sushi         |
""
```

<img width="550" alt="Table numbering" src="https://github.com/user-attachments/assets/b793205e-629f-414a-bee1-780daf636d87">


&nbsp;

# Custom numbered elements

Along with built-in numerable elements we just discussed, Quarkdown additionally allows any element to be numbered if wrapped in a `.numbered` block.

The function accepts two arguments:
1. A key string. The number of the element is counted across previous occurrences with the same key;
2. A [lambda](lambda) block which takes the number as an argument, formatted according to the active numbering format.

```markdown
.numbered {greetings}
  number:
  **Hello!** This block has the number **.number**
```

Executing the previous block will render an empty string in place of `number`.
That's because we need to specify the numbering format for `greetings` in the `.numbering` call:

```yaml
.numbering
  ...
  - greetings: 1.a
```

Full example:

```markdown
.numbering
    - headings: 1.1
    - greetings: 1.a

# Title 1

.numbered {greetings}
    number:
    **Hello!** This block has the number **.number**

.numbered {greetings}
    number:
    **Hey!** This has instead the number **.number**

# Title 2

.numbered {greetings}
    number:
    **Hi!** Here we have the number **.number**
```

<img width="600" alt="Custom numbering" src="https://github.com/user-attachments/assets/7df10490-4e3d-42f5-aa82-879a840d2be3">

&nbsp;

# Localization

The localized name of the labeled element appear in captions if [`.doclang`](document-metadata) is set and the locale is supported.  
For instance *Figure* and *Table* for the English locale, *Figura* and *Tabella* for Italian.

&nbsp;

# Themes

[Layout themes](theme) affect the way numbers are displayed:

<img width="550" alt="Minimal headings numbering" src="https://github.com/user-attachments/assets/a029b9aa-c2ac-4de4-ab89-8b8fe2221403">

<img width="550" alt="Minimal ToC numbering" src="https://github.com/user-attachments/assets/86edb07c-0c1f-4258-b827-7e9d6321d200">


> `minimal` theme
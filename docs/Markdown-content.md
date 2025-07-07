Many functions accept rich ~Mark~*Quark*down content as their argument.

# Block content

Usually accepted by body parameters, *block content* refers to one or more *block* element that Quarkdown supports. This includes paragraphs, headings, code blocks, quotes, [block function calls](syntax-of-a-function-call#block-vs-inline-function-calls), etc.  
Inner *inline* element is, of course, processed as well.  

In other words, everything you can express with Quarkdown *outside* a function call, will also work here.

```markdown
.center
  # My centered title

  This is a paragraph in a **centered** block!

  > This is a _blockquote_.
  >
  > It spans over multiple sub-paragraphs.

  <!-- A nested block function call -->
  .row
    ...
```
> See more: [`.center`](align), [`.row`](stacks)

# Inline content

*Inline content* strictly accepts inline data, ignoring any block syntax. This includes plain text, strong (bold), emphasis (italics), code spans, links, images, [inline math](tex-formulas), [inline function calls](syntax-of-a-function-call#block-vs-inline-function-calls), etc.

```markdown
.box {My _box_ title}
  ...
```
> See more: [`.box`](box)

Block syntax has no effect where inline content is required. In the following example, *# My box* is parsed as plain text, since headings are blocks.

```markdown
.box {# My box}
  ...
```

Inline function calls are accepted:

```markdown
.box {3 + 2 is .sum {3} {2}}
  ...
```
> See more: [`.sum`](math)

In general, everything that can be put inside a paragraph can go into an inline argument as well.

```markdown
This is the link to .text {[Quarkdown](https://github.com/iamgio/quarkdown)} size:{large}
```
> <img width="300" alt=".text result" src="https://github.com/user-attachments/assets/21d8b056-0bb7-4d84-ac16-3b70d55e39a3">  
>
> See more: [`.text`](text)

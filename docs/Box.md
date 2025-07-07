The **`.box`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Layout/box.html)</sup> allows creating a special *box* container.

A box features an inline *title* and block *content*.

```markdown
.box {Box title}
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.
```
> <img width="600" alt="Box result" src="https://github.com/user-attachments/assets/5b99cca2-ae0c-4cbe-bba2-1a9876980401">

&nbsp;

The title can be omitted:

```markdown
.box
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.
```

> <img width="600" alt="Title-less box" src="https://github.com/user-attachments/assets/2cb134e7-f01a-4cbe-adcb-6e4a4ed34121">

&nbsp;

A box can have a type, which is `callout` by default, if not specified. Available types are:
- `callout`
- `tip`
- `note`
- `warning`
- `error`

```markdown
.docname {Test}
.docauthor {iamgio}
.doclang {english}
.doctype {paged}
.theme {darko} layout:{minimal}

.box {Box title} type:{tip}
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.

.box {Box title} type:{note}
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.

.box {Box title} type:{warning}
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.
```
> <img width="600" alt="Typed boxes" src="https://github.com/user-attachments/assets/28d4f78c-45c7-41ae-9c40-5927f44aefed">

&nbsp;

If the title is omitted, [`.doclang`](document-metadata) is set and the set locale is supported, the box title is automatically [localized](localization).

```markdown
.box type:{tip}
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.

.box type:{note}
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.

.box type:{warning}
  Welcome to the **Quarkdown wiki**!  
  Here you'll learn how to get started with your first document.
```
> <img width="600" alt="Typed title-less boxes" src="https://github.com/user-attachments/assets/fca7ef6f-bb26-4c7d-b087-9ca4a198bf62">

&nbsp;

> [!TIP]
> Boxes and [typed quotes](quote-types) are different ways to achieve typed alerts.

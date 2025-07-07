Quarkdown introduces the concept of **figure**, which is missing in base Markdown. A figure wraps an image and is horizontally centered.

<img width="600" alt="Demo: about Quarkdown's logo" src="https://github.com/user-attachments/assets/e82f9afd-daf8-49e8-b6a8-51b8bd21716e">

&nbsp;

If a paragraph only consists of a single image (in other words: an isolated image), then it becomes a figure.

```markdown
Lorem ipsum dolor sit amet, consectetur adipiscing elit.

![...](img.png)

Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

If the image contains a *title* attribute (wrapped in double quotes, single quotes or parentheses), it is displayed as a caption.

```markdown
![Logo](quarkdown-icon.svg "The Quarkdown icon.")
```

The [image size](image-size) feature works on figures as well.

Figures can be **numbered**: see [Numbering](numbering) for further information.

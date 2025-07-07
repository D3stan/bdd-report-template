The **`.figure {caption?} {body}`** adds generalization to the [image figures](figure) syntax extension, as it allows for any content to be handled as a *figure* block, which:
- May feature a caption;
- Can be numbered (see [*Numbering*](numbering)).

```markdown
# Custom figures

.figure {My caption.}
    .container padding:{1cm} background:{yellow}
        Hello, world!
```

<img width="600" alt="Custom figure" src="https://github.com/user-attachments/assets/f851d83b-a1a9-460e-8eec-fd9c7b757292" />


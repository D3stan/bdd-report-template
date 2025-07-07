The **`.paragraphstyle`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Document/paragraphstyle.html)</sup> function makes it possible to override the global style of paragraphs.

Its parameters are optional and, if unset, they delegate their value to the active theme.

| Parameter | Description | Accepts |
|-----------|-------------|---------|
| `lineheight` | Whitespace between lines, multiplied by the font size. | Number |
| `letterspacing` | Whitespace between letters, multiplied by the font size. | Number |
| `spacing` | Whitespace between subsequent paragraphs, multiplied by the font size. | Number |
| `indent`  | Whitespace at the start of each non-first paragraph, multiplied by the font size. | Number |

Using `spacing:{0} indent:{2}` will provide the classic LaTeX look.

---

Default appearance:

<img width="600" alt="Default" src="https://github.com/user-attachments/assets/5fac5aa7-8d64-4aaa-8b93-6585476b54f3" />

&nbsp;

```
.paragraphstyle lineheight:{2.5} spacing:{0} indent:{2}
```

<img width="600" alt="Customized" src="https://github.com/user-attachments/assets/76eb2038-54eb-45fa-bf23-ac20b391f23e" />

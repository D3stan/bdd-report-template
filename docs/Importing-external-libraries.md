The **`.include`** function, previously seen in [*Including other Quarkdown files*](including-other-quarkdown-files), does not only import project files, but also external **libraries**.

When downloading Quarkdown or building it via `distZip`, the `lib/qmd` directory contains utility libraries written in Quarkdown itself.

```
quarkdown/
├─ lib/qd/
│  ├─ lib.qd
│  ├─ ...
├─ bin/
│  ├─ quarkdown.jar
```

The `.qmd` files can be easily imported into a Quarkdown project via `.include {name}` which, contrary to the other usage, does not expect a file extension.

If we want to import the example `lib.qd`, `.include {lib}` will get the job done.

> [!NOTE]
> Contrary to `.include {path}`, this approach only loads declared symbols, and does not append Markdown content from the file.

The default directory to load libraries from defaults to `<install directory>/lib/qmd`, and can be overridden via the command-line option `-l` or `--libs`.
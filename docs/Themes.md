A theme defines the look and feel of your Quarkdown document. More themes are to come in the future.

Themes are split in two groups: *color* themes, which define the color scheme of a document, and *layout* themes, which set the general structural rules of the layout.    
Combining them can create a document that truly stands out.

A theme can be set via the **`.theme {colortheme} layout:{layouttheme}`** function.

### Color themes
- `paperwhite` (default)
- `darko`
- `beaver`

### Layout themes
- `latex` (default)
- `minimal`
- `beamer`

---

Some suggested combinations are:
- `darko+minimal` (used by the [demo presentation](https://iamgio.eu/quarkdown/demo/))
- `paperwhite+latex` (LaTeX look, great for `paged` documents)
- `beaver+beamer` (Beamer look, great for academic-style presentations).

# Contributing

[Theme contributions](https://github.com/iamgio/quarkdown/tree/main/quarkdown-html/src/main/resources/render/theme) are welcome!

Please make sure they work well with all the three document types before submitting.  
The [Mock document](https://github.com/iamgio/quarkdown?tab=readme-ov-file#mock-document) is a great way to test themes.
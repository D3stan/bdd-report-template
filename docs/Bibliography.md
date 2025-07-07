Quarkdown provides first-class bibliography generation with out-of-the-box [BibTeX](https://www.bibtex.org) compatibility.

To get started, invoke the **`.bibliography {file.bib}`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Bibliography/bibliography.html)</sup> function, with `file.bib` being the path to the `.bib` file.  
You may find some BibTeX examples [here](https://www.bibtex.com/e/entry-types/).

```
.bibliography {file.bib}
```

<img width="671" alt="Bibliography" src="https://github.com/user-attachments/assets/3bd64c2e-3af9-4f00-abf1-e343c5e066ab" />

&nbsp;

# Citations

An entry of a bibliography can be cited via the **`.cite {key}`** function.

Considering the following Bib entry:

```bibtex
@article{einstein,
  author = "Albert Einstein",
  ...
}
```

Then it can be cited by means of the `einstein` key:

```
Einstein's publication .cite {einstein} in 1905 revolutionized the field of physics.  
Similarly, Hawking's book .cite {hawking} has had a profound impact
on our understanding of cosmology and black holes.
```

<img width="671" alt="Citation" src="https://github.com/user-attachments/assets/3f098484-9853-4ba3-9fc1-fa02369dbf3e" />

&nbsp;

# Style

The optional `style` parameter, which defaults to `plain`, configures the look and format of the bibliography and its citation references. Styles are directly inspired by LaTeX's and comprehensive comparisons can be found [here](https://www.overleaf.com/learn/latex/Bibtex_bibliography_styles).

Here are the currently supported styles:

- **`plain`**

  <img width="600" alt="plain style" src="https://github.com/user-attachments/assets/be2db3c2-17f2-4672-b1fb-ffa3565c902e" />

- **`ieeetr`**

  <img width="600" alt="ieeetr style" src="https://github.com/user-attachments/assets/efb5e39a-1d4c-4a0a-90cc-5047c4db2af0" />


- **`acm`**

  <img width="600" alt="acm style" src="https://github.com/user-attachments/assets/3436780f-3f95-463f-bb80-6a8d0e3c0cae" />

&nbsp;

# Title

By default, the title will be [localized](localization) to the current locale set via `.doclang`, if supported. A custom title can be set via the `title` parameter:

```
.bibliography {file.bib} title:{My bibliography}
```

<img width="671" alt="Custom title" src="https://github.com/user-attachments/assets/28034ff9-9cd0-4ab1-adfe-0887ee2265ac" />

&nbsp;

Depending on the current [auto page break](page-break#automatic-break) configuration, the title will likely cause a page break. Page breaks can be prevented by turning the title to a [decorative heading](decorative-headings) by means of the `decorativetitle` parameter:

```
.bibliography {file.bib} title:{My bibliography} decorativetitle:{yes}
```


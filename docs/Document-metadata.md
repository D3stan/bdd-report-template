Information about the document can be set via functions. These functions should conventionally be called at the beginning of a Quarkdown source.

| Name | Accepts | Default |
|------|---------|---------|
| `.docname`   | The name of the document. | `Untitled Quarkdown Document` |
| `.docauthors` | The authors of the document. | (empty)                   |
| `.doctype`   | Type of output document: `plain`, `slides`, `paged`.   | `plain` |
| `.doclang`   | <p>Language of the document: either a case-insensitive English full name (e.g. `English`, `Italian`, `French (Canada)`) or a IETF BCP 47 language tag (e.g. `en`, `it`, `fr-CA`).</p><p>This defines:<ul><li>The target locale to localize content to.</li><li>Locale-specific styles, such as a Chinese font loaded only for Chinese locales.<li>HTML's `lang` attribute, which enables hyphenation and enhances accessibility.</li></ul></p><p>See [Localization](localization) for more.</p> | (none) |

All these functions have a *'modify or echo'* behavior: if the value is not passed as an argument, then they return the previously set value. Example:
```markdown
.docname {Quarkdown}

This document is called **.docname**!
```
> This document is called **Quarkdown**!

# Authors

`.docauthors` sets the document's authors.

```
.docauthors
  - John Doe
  - Jane Doe
```

The function takes a [Dictionary](dictionary) as its value, where each key is the author's name, while values are nested dictionaries which represent the author's information. No constraints are set and any information entry can be used.

```
.docauthors
  - John Doe
    - email: johndoe@example.com
    - website: example.com
  - Jane Doe
    - email: janedoe@example.com
    - company: GitHub
```

Calling the same function with no arguments returns the dictionary itself, which may for example be iterated on to automatically display the authors according to a certain layout. The following example takes advantage of *pair [destructuring](destructuring)*:

```
.foreach {.docauthors} 
    name info:
    .row gap:{1cm}
        **.name**

        .get {email} from:{.info}
```

<img width="550" alt="Authors layout" src="https://github.com/user-attachments/assets/99136a4e-451f-4089-bb14-899cebb5def1" />


## Single author

If the document has just one author and no further information is needed, the **`.docauthor {name}`** function is a valid shorthand.  

Be the author defined via `.docauthors` or `.docauthor`, calling `.docauthor` with no arguments returns the only author's name.
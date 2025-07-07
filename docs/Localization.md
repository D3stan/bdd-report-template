Quarkdown supports **string localization** out of the box.

The first step is to set the document language via [**`.doclang {locale}`**](document-metadata) and it's suggested to call it among the other document metadata (such as `.docname`, `.docauthor`, etc.).  

`locale` can be represented as either a case-insensitive English full name (e.g. `English`, `Italian`, `French (Canada)`) or a IETF BCP 47 language tag (e.g. `en`, `it`, `fr-CA`).

&nbsp;

# Built-in localization

Quarkdown's built-in libraries expose localization tables that allow localization of elements such as [quote types](quote-types), [numbering](numbering) captions, and [table of contents](table-of-contents) title.

> [!NOTE]
> The currently supported locales are **English, Italian, German, Chinese and Japanese**.
>
> Contributions to support new locales are welcome:
> - [stdlib](https://github.com/iamgio/quarkdown/blob/main/quarkdown-stdlib/src/main/resources/lib/localization.qmd)
> - [paperlib](https://github.com/iamgio/quarkdown/blob/main/quarkdown-libs/src/main/resources/paper.qmd) 

&nbsp;

# Creating your own localized strings

Imagine a function `.theorem` that displays the paragraph name **`Theorem. `**, LaTeX style:

```
.function {theorem}
    **Theorem.**

.theorem This is my theorem...
```

> Output:  
> **Theorem.** This is my theorem...

<br>

This is great if you're making it for your own English document, but what if you're making a library for everyone to use? You'd need to support multiple languages. This is where *localization tables* come in.

The `.localization {name}` function defines a new **localization table** associated with a unique name.
Its body parameter accepts a particular Markdown unordered list that, in Quarkdown, is called a [*dictionary*](dictionary).

This localization dictionary exposes key-value pairs for each locale that you intend to support.  
The locale names follow the same rules as the ones from `.doclang`, hence they can be full names or tags.

```
.localization name:{mylib}
  - English
    - theorem: Theorem
  - Italian
    - theorem: Teorema
```

As long as `.doclang` is set, the localized string can be accessed via `.localize {table:key}`, in this case `.localize {mylib:theorem}`.

The previous function would now look like this:

```
.function {theorem}
    **.localize {mylib:theorem}.**

.theorem This is my theorem...
```

&nbsp;

# Extending a built-in localization table

If your locale is not yet supported by Quarkdown and you're unable to contribute to the project, it is still possible to extend the built-in localization tables for your document.

When calling `.localization {name}`, an additional **`merge:{yes}`** argument will cause the localization table with the given name to be extended with the new user-provided one. Any conflicting entries will be replaced by the new ones.

For instance, [typed boxes](box) feature a localized title by default, such as *Warning* for a warning-typed box.
If the document locale is not supported, the title will be missing.  
In order to extend the built-in localization with box titles in Canadian French, the following approach can be used:

```
.localization {std} merge:{yes}
    - fr-CA
      - warning: Avertissement
      - error: Erreur
      ...
```

After that, assuming Canadian French is set in `.doclang`, the new entries will be available to the `.box` function.

Built-in table names and entries are listed in this page's [*Built-in localization*](#built-in-localization).
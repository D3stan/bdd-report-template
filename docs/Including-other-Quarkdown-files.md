The **`.include {file}`** function makes it possible to load and evaluate an external Quarkdown source file.

Its parameter accepts a string which represents the **path to the target file**, which may be relative to the location of the main source file, or absolute.

> To include external libraries, please refer to [*Importing external libraries*](importing-external-libraries).

You can think of it **as if the content of the target file was inserted in place of the function call**.  

> `a.qd`
> ```
> ### Hello Quarkdown
>
> This is external content.
> ```

> `main.qd`
> ```
> .include {a.qd}
> ```
> Output:
>
> ### Hello Quarkdown
>
> This is external content.

&nbsp;

# Context sharing

Any information about the context and environment is automatically inherited and can be modified by the included files.  
This means declared functions and variables are imported as well in the main file.

> [!TIP]
> You can take this to your advantage to make awesome libraries!

> `a.qd`
> ```
> .function {greet}
>   name:
>   Hello, **.name**!
> ```

> `main.qmd`
> ```
> .include {a.qd}
>
> .greet {John}
> ```
> Output:
>
> Hello, **John**!

> [!CAUTION]
> Circular dependency results in an error.

&nbsp;

# Bulk include

A clean approach with using typesetting systems would be having a main file which gathers all the different subfiles together.  
For this purpose, the `.includeall` function, which takes an [Iterable](iterable) of paths, comes particularly handy as a shorthand for repeated `.include` calls.

The following snippet is taken from [Mock](https://github.com/iamgio/quarkdown/blob/main/mock)'s `main.qd` file:

```
.includeall
    - setup.qd
    - headings.qd
    - paragraphs.qd
    - lists.qd
    - images.qd
    - tables.qd
    - code.qd
    - textformatting.qd
    - colorpreview.qd
    - quotes.qd
    - boxes.qd
    - math.qd
    - mermaid.qd
    - collapsibles.qd
    - errors.qd
    - separators.qd
    - alignment.qd
    - stacks.qd
```

&nbsp;

# Use case: setting up

A common use case would be putting all the setup function calls in a separate file (see the *Setting up* section of this wiki to see all).

> `setup.qd`
> ```
> .docname {My document}
> .docauthor {iamgio}
> .doctype {slides}
> .doclang {English}
> .theme {darko} layout:{minimal}
> 
> .footer
>    ...
> ```

> `main.qd`
> ```
> .include {setup.qd}
>
> # My cool document
> 
> ...
> ```
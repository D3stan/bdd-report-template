**Functions** are the key feature of Quarkdown, distinguishing it from other Markdown dialects and many other markup languages. They are loaded from external libraries, either native (e.g. [stdlib](https://github.com/iamgio/quarkdown/tree/main/stdlib/src/main/kotlin/eu/iamgio/quarkdown/stdlib)) or defined in a Quarkdown source, and come in different categories.

| Category                           | Examples                                                    |
|------------------------------------|-------------------------------------------------------------|
| Layout rules                       | `row`, `column`, `grid`, `center`                           |
| Utility views                      | `tableofcontents`, `whitespace`                             |
| Mathematical and logical operations| `sum`, `divide`, `pow`, `sin`, `isgreater`                  |
| Control structures and statements  | `if`, `foreach`, `repeat`, `var`, `let`, `function`          |
| File data                          | `include`, `csv`, `read`                                    |
| Alteration of document metadata    | `docname`, `docauthor`, `doctype`, `theme`, `pageformat`    |

And more...

When called from a Quarkdown source, the function name is preceded by a `.` (dot) and each argument is wrapped in curly brackets. 

```
.myfunction {arg1} {arg2}
```

In the previous example, `arg1` and `arg2` refer to, respectively, the first and second parameter of the function signature, hence the name *positional argument*. An argument can also refer to a parameter by name (*named argument*) with the syntax `name:{arg}`.

```
.myfunction firstparam:{arg1} secondparam:{arg2}
```

Positional and named arguments can be mixed to improve readability of the function call, as long as all the arguments that follow a named argument are named as well.

```
.multiply {6} by:{3}
```

> This is more natural and readable than `.multiply {6} {3}`


Arguments can span over multiple lines. Indentation is optional and arbitrary.

```
.divide {
  .cos {.pi}
} by:{
  .sum {2} {1}
}
```

Function calls can be nested in arguments:

```
.multiply {.pow {3} to:{2}} by:{.pi}
```

# Chaining calls

Although Quarkdown exclusively relies on top-level declarations, it exploits some OOP-like syntactic sugar that greatly increases the readability of nested function calls.

Imagine the following call:

```
.sum {.subtract {.pow {3} {2}} {1}} {2} 
```

This performs $(3^2 - 1) + 2 = 10$. As simple as it is, it couldn't be harder to write and read!  
The following call is totally equivalent to the previous one:

```
.pow {3} {2}::subtract {1}::sum {2}
```

Much, much better. It now resembles the way we naturally read math.

To understand how it works, consider this simpler call (see [*Variables*](variables) to learn more about variables):

```
.myvar::uppercase
```

What the compiler does, behind the scenes, is transforming the previous call into the following:

```
.uppercase {.myvar}
```

Generally speaking, `.a::b` is transformed into `.b {.a}`, `.a::b::c` into `.c {.b {.a}}` and so on.

Additional arguments can be appended to any function of the chain. Just keep in mind that the chained value is always **the first argument**, positionally speaking, of the next call.

`.a {x}::b {y}` is transformed into `.b {.a {x}} {y}`.

Many core functions are designed to be called in a chain, for example [`None` operations](none#examples).

# Block vs. inline function calls

An **inline** function call is preceded and/or followed by other inline content, such as text and images.  
The output of an inline function call is simply inserted in the parent's block.

> ```
> Ever wondered what **26+16** equals? It's .sum {26} {16}. Here you go.
> ```
> HTML rendering:
> ```html
> <p>Ever wondered what <strong>26+16</strong> equals? 42. Here you go.</p>
> ```

A **block** function call is an isolated one. For context, a *block* is a paragraph, a code snippet, a quote, etc.

```
Paragraph 1

.myfunction {arg1} {arg2}

Paragraph 2
```

The output of a block function call may or may not be wrapped into a paragraph depending on its type. For instance, a string or number value is wrapped, whereas a layout element (e.g. `.row`) is not.

The main difference between inline and block function calls, however, is a special argument called **body argument**, which **always** refers to the **last parameter** of the signature (even if named arguments were used).

A body argument expands over multiple lines, it's not wrapped by brackets and requires each line to be **indented** by at least two spaces or one tab:

```
.myfunction {arg1} {arg2}
  Body argument, line 1
  and line 2.
```

The whole body must share the same indentation:

```html
.myfunction {arg1} {arg2}
  Body argument, line 1
      and line 2. <!-- This is a 4-spaces indented code block! -->
```

Functions, block or inline, can be nested inside body arguments:

```html
.row alignment:{center}                <!-- Block  -->
  This document was made by .docauthor <!-- Inline -->

  .column                              <!-- Block  -->
    The document name is .docname      <!-- Inline -->

    .loremipsum                        <!-- Block  -->
```

When nested inside inline arguments, function calls are always inline. Thus, this is invalid since body arguments are accepted only in block calls:

```
.center {
  .row
    Hi
}
```

While this is valid as `.row` is called within a body argument:
```
.center
  .row
    Hi
```
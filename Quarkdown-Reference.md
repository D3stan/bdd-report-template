# Quarkdown Technical Reference

---

## Table of Contents

1. [CLI Tools](#cli-tools)
2. [Advanced Features](#advanced-features)
3. [Data Types and Value Types](#data-types-and-value-types)
4. [Built-in Libraries](#built-in-libraries)
5. [Native Content Integration](#native-content-integration)
6. [Technical Implementation](#technical-implementation)
7. [Configuration and Environment](#configuration-and-environment)
8. [Utilities and Advanced Functions](#utilities-and-advanced-functions)
9. [Slides and Presentations](#slides-and-presentations)
10. [Localization and Internationalization](#localization-and-internationalization)

---

## CLI Tools

### Compiler

The main Quarkdown compiler processes `.qmd` files and converts them to various output formats.

**Basic Usage:**
```bash
quarkdown compile input.qmd
```

**Options:**
- `--output <file>` - Specify output file name
- `--format <format>` - Output format (html, pdf)
- `--theme <theme>` - Apply a specific theme
- `--watch` - Watch for file changes and recompile

### PDF Export

When running Quarkdown's compiler via `quarkdown c`, specifying the **`--pdf`** flag generates a PDF file.

- The content of the PDF matches 1:1 with what the HTML output would render in the Chrome browser
- All document types and features supported by the HTML target are also supported

#### Requirements 

In order to generate PDF files from HTML, the following dependencies are required:
- Node.js
- npm (usually bundled with Node.js)
- [Puppeteer](https://pptr.dev) (`npm install puppeteer --prefix <quarkdown_dir>/lib`)

Dependencies are already taken care of by package managers and install scripts.

#### Additional Options

- `--node-path <path>`: sets the path to the Node.js executable. Defaults to `node`
- `--npm-path <path>`: sets the path to the npm executable. Defaults to `npm`
- `--pdf-no-sandbox`: disables Chrome sandbox during PDF generation. This is potentially unsafe and should be used only when strictly needed

#### Environment Variables

- `QD_NPM_PREFIX`: directory where `node_modules` should be found. Defaults to `lib` if Quarkdown was installed via a package manager or install script
- `PUPPETEER_EXECUTABLE_PATH`: path to the Chrome/Chromium/Firefox executable
- `PUPPETEER_BROWSER`: `chrome`/`firefox`. Defaults to the automatically found browser

#### Manual Export (Legacy)

An HTML artifact can be exported to PDF via the **in-browser print** feature (`CTRL/CMD + P`). 

While `paged` (and `plain`) documents are print-ready, you'll need a few additional steps to save your `slides` document as PDF. Please refer to [Reveal's instructions](https://revealjs.com/pdf-export/#instructions) to learn how to do so.

### Project Creator

Bootstrap new Quarkdown projects with predefined templates and structures.

### Webserver

Start a local development server for live preview and hot reloading of Quarkdown documents.

---

## Advanced Features

### Dynamic Typing

Quarkdown employs **dynamic typing**: the type of a value is resolved at evaluation time rather than being declared.

#### Type Resolution

The type of a value is automatically inferred based on its content and context. For example:

```
.var {myvalue} {Hello world}  <!-- String -->
.var {myvalue} {42}           <!-- Number -->
.var {myvalue} {yes}          <!-- Boolean -->
```

#### Context-Sensitive Adaptation

Values automatically adapt to their context. For instance, a string containing Markdown will be parsed as rich content when used in a content context, but remain as plain text when used in a code block.

Example from a function that shows source and result:

```html
.function {sourceresult}
  source:
  .code {markdown}
    .source
  .source
```

What this example shows is how versatile Quarkdown values are. In the function declaration, the `.source` argument is retrieved twice:
- In `.code`, which expects a string, so the source is read as-is and inserted in a code block
- At the top level: the Quarkdown source is automatically adapted to the context, so it's parsed as rich Markdown content

### Importing External Libraries

Extend Quarkdown functionality by importing external libraries and modules.

```
.import {library-name}
```

### Localization

Quarkdown supports internationalization through locale-specific content and automatic text translation.

#### Setting Document Language

```
.doclang {en-US}
```

#### Localization Tables

Define locale-specific content using dictionaries:

```yaml
.localization
  - English:
    - greeting: Hello
    - farewell: Goodbye
  - Italian:
    - greeting: Ciao
    - farewell: Arrivederci
```

#### Accessing Localized Content

```
.locale {greeting}
```

### TeX Macros

Define reusable TeX macros for mathematical expressions:

```latex
.texmacro {\hello}
    \text {Hello, \textit {world}}

.texmacro {\highlight}
    \colorbox{yellow}{#1}

$ \highlight{\hello} $
```

#### Composing Macros

Multiple macros can be defined and combined:

```latex
.texmacro {\hello}
    \text {Hello, \textit {world}}

.texmacro {\highlighthello}
    \colorbox{yellow}{\hello}

$ \highlighthello $
```

---

## Data Types and Value Types

### String

Text values that can contain Unicode characters and support various string manipulation functions.

**String Manipulation Functions:**
- `.upper {text}` - Convert to uppercase
- `.lower {text}` - Convert to lowercase
- `.capitalize {text}` - Capitalize first letter
- `.length {text}` - Get string length
- `.substr {text} {start} {end}` - Extract substring

### Number

Numeric values supporting arithmetic operations and mathematical functions.

**Math Operations:**
- `.sum {a} {b}` - Addition
- `.sub {a} {b}` - Subtraction  
- `.mul {a} {b}` - Multiplication
- `.div {a} {b}` - Division
- `.mod {a} {b}` - Modulo
- `.pow {base} {exponent}` - Exponentiation
- `.sqrt {number}` - Square root
- `.abs {number}` - Absolute value

### Boolean

Boolean values are represented by the following literals (**case insensitive**):

| Boolean value | Literals |
|---------------|----------|
| **`true`**  | `true`, `yes` |
| **`false`** | `false`, `no` |

It is encouraged to use the `yes`/`no` literals as they contribute towards the 'natural language flow' of the language.

Example:
```
.code linenumbers:{no}
  My code
```

#### Boolean Operators

A `Boolean` is returned by the following operator functions:
- `.not {bool}` - Negation (chaining suggested: `.bool::not`)
- `.islower {a} {than}` - Less than comparison
- `.isgreater {a} {than}` - Greater than comparison
- `.isequal {a} {to}` - Equality comparison

### Markdown Content

Rich content that preserves Markdown formatting and can be processed as structured text.

### None

Represents absence of value, similar to null or undefined in other languages.

```
.var {emptyvalue} {.none}
```

### Enumeration Entry

Represents a specific value from a defined enumeration set.

### Iterable

Ordered lists or unordered sets that can be iterated through loops.

#### Collection

An ordered or unordered Markdown list is automatically converted to an ordered collection:

```markdown
.var {letters}
  - A
  - B
  - C

.foreach {.letters}
  .1::lowercase
```

#### Nested Collections

```markdown
.var {letters}
  - - A
    - B
  - - C
    - D
  - - E
    - F

.foreach {.letters}
  .1::first
```

#### Pair

A pair is an iterable of two values:

```
.pair {first} {second}
```

#### Operations

Useful operations can be accessed via function call chaining as `.myiterable::operation`:

- `.myiterable::getat {index}` - Get element at index
- `.myiterable::sorted` - Sort collection
- `.myiterable::average` - Calculate average (for numeric collections)
- `.myiterable::first` - Get first element
- `.myiterable::last` - Get last element
- `.myiterable::size` - Get collection size

For a complete list, refer to the stdlib's [`Collection` documentation](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Collection).

### Dictionary

A collection of key-value pairs without duplicate keys. A key is always a string value, while a value can be of any type.

The syntax for dictionaries recalls the YAML one:

```yaml
- key1: value1
- key2: value2
- key3: value3
```

#### Explicit Dictionary Declaration

```yaml
.var {mydictionary}
  .dictionary
    - key1: value1
    - key2: value2
    - key3: value3
```

#### Nested Dictionaries

```yaml
- English:
  - greeting: Hello
  - food: Fish and chips
- Italian:
  - greeting: Ciao
  - food: Pasta
```

Trailing colons are optional:

```yaml
- English
  - greeting: Hello
  - food: Fish and chips
- Italian
  - greeting: Ciao
  - food: Pasta
```

### Range

The syntax to define a range is **`a..b`**, with `a` and `b` non-negative integers.

#### Range Types

- **Closed range**: `a..b`
- **Open on the left end**: `..b`
- **Open on the right end**: `a..`
- **Open on both ends**: `..`

#### Dynamic Range Creation

The `..` operator is syntactic sugar for the **`.range {from} {to}`** function:

```
.range {.start} {.end}
```

### Lambda

A lambda is a block of code that maps parameters to a single output value.

#### Syntax

```
param1 param2 param3:
My code
```

#### Parameter Access

Parameters can be accessed as variables:

```
param1 param2 param3:
The second parameter is .param2
```

#### Implicit Parameters

When the header is omitted, parameters become implicit:

```
The second parameter is .2
```

#### Inline Lambda

For inline arguments, use the **`@lambda`** instruction:

```
.myfunction {@lambda x y: The values are .x and .y}
```

Or with implicit parameters:

```
.myfunction {@lambda The values are .1 and .2}
```

#### Scope

Lambdas create new **scopes**:
- Nested scopes inherit properties from their parent
- Properties defined inside a nested scope cannot be accessed by their parent

### Sizes

Define dimensions using various units:

- **Pixels**: `100px`
- **Centimeters**: `5cm`
- **Inches**: `2in`
- **Millimeters**: `15mm`
- **Percentages**: `50%`
- **Points**: `12pt`

### Color

Define colors using various formats:

- **Named colors**: `red`, `blue`, `green`
- **Hex colors**: `#FF0000`, `#00FF00`
- **RGB**: `rgb(255, 0, 0)`
- **RGBA**: `rgba(255, 0, 0, 0.5)`
- **HSL**: `hsl(0, 100%, 50%)`

---

## Built-in Libraries

### Paper Library

The Paper library provides academic document formatting with abstract, definitions, theorems, and more.

#### Abstract

Create document abstracts:

```
.abstract
  This document presents...
```

#### Definitions

Define terms with formal definitions:

```
.definition {Algorithm}
  A step-by-step procedure for solving a problem.
```

#### Theorems

State mathematical theorems:

```
.theorem {Pythagorean Theorem}
  In a right triangle, the square of the hypotenuse equals the sum of squares of the other two sides.
```

#### Proofs

Provide mathematical proofs:

```
.proof
  Let a and b be the lengths of the legs...
  Therefore, a² + b² = c².
```

---

## Native Content Integration

### HTML Integration

Standard Markdown specifications allow freely mixing Markdown and HTML, but Quarkdown encourages **target agnosticism** for rendering consistency across all supported targets.

#### HTML Function

As a last resort, use the `.html` function for direct HTML injection:

```markdown
**Hello** .html {<em>world</em>}!
```

```markdown
.html
  <div class="my-container">
    My HTML container
  </div>
```

> [!WARNING]
> - The rendered output is unsanitized content, possibly vulnerable
> - This approach is not target-agnostic, as other rendering targets will ignore the provided content

#### Alternative Approaches

Quarkdown provides dedicated functions for common HTML workarounds:

**Collapsible blocks** instead of HTML `<details>`:
```markdown
.collapsible {Title of the collapsible block}
  Content of the collapsible block.
```

---

## Technical Implementation

### Pipeline Architecture

When an input file is supplied to Quarkdown, it undergoes a sequential pipeline process:

1. **Lexing** - Tokenization of input text
2. **Parsing** - Building abstract syntax tree
3. **Function call expansion** - Processing function calls
4. **Tree traversal** - Walking the syntax tree
5. **Rendering** - Converting to target format
6. **Post-rendering** - Final processing and optimization

Each stage takes the output of the previous stage as input, creating a clean separation of concerns.

### Media Storage

The media storage system handles **both local and remote files**:

- **HTML rendering**: enabled for local files only
- **LaTeX rendering** (future): requires remote media to be downloaded locally

Overriding these rules is supported but currently unavailable via CLI.

---

## Configuration and Environment

### Document Types

Quarkdown supports multiple document types:

- **`paged`** - Traditional paginated documents
- **`slides`** - Presentation slides
- **`plain`** - Simple documents without pagination

### Themes

Apply visual themes to documents:

```
.theme {material}
.theme {academic}
.theme {minimal}
```

### Custom Figure Styling

Create custom figure layouts and styling:

```
.figure alignment:{center} caption:{bottom}
  ![Image](image.png)
```

### Clip Regions

Define clipping areas for content:

```
.clip region:{circle}
  Content to be clipped
```

---

## Utilities and Advanced Functions

### Text Processing

#### Advanced Text Formatting

```
.text color:{red} size:{large} weight:{bold} family:{serif}
  Styled text
```

#### Text Transformation

- `.upper {text}` - Convert to uppercase
- `.lower {text}` - Convert to lowercase  
- `.capitalize {text}` - Capitalize first letter
- `.reverse {text}` - Reverse string
- `.trim {text}` - Remove whitespace

### Code Block Enhancement

Enhanced code blocks with additional features:

```
.code language:{python} linenumbers:{yes} highlight:{2,5} theme:{dark}
  def fibonacci(n):
      if n <= 1:          # Highlighted
          return n
      else:
          return fibonacci(n-1) + fibonacci(n-2)  # Highlighted
```

### Table Operations

Advanced table manipulation:

```
.table
  | Name | Age | City |
  |------|-----|------|
  | John | 25  | NYC  |
  | Jane | 30  | LA   |
::sort {Age}
::filter {Age > 25}
::compute {Average Age} {.average {Age}}
```

### Custom Figure Creation

Create figures with custom layouts:

```
.figure type:{custom} layout:{grid}
  ![Image 1](img1.png)
  ![Image 2](img2.png)
  ![Image 3](img3.png)
```

---

## Slides and Presentations

### Slides Configuration

Configure slide presentation settings:

```
.slides center:{yes} controls:{yes} transition:{fade} speed:{fast}
```

#### Configuration Options

| Parameter | Description | Accepts | Default |
|-----------|-------------|---------|---------|
| `center` | Whether content should be centered vertically | [`Boolean`](boolean) | Theme dependent |
| `controls` | Whether navigation controls should be shown | [`Boolean`](boolean) | `true` |
| `transition` | Transition style between slides | `none`, `fade`, `slide`, `zoom` | `slide` |
| `speed` | Transition speed between slides | `default`, `fast`, `slow` | `default` |

### Interactive Fragments

Create slide fragments that appear progressively:

```
.fragment
  First fragment

.fragment
  Second fragment

.fragment
  Third fragment
```

#### Fragment Types

- **Appear**: `.fragment {appear}`
- **Fade in**: `.fragment {fade-in}`
- **Fade out**: `.fragment {fade-out}`
- **Highlight**: `.fragment {highlight}`

---

## Localization and Internationalization

### Setting Document Language

```
.doclang {en-US}
.doclang {it-IT}
.doclang {fr-FR}
```

### Creating Localization Tables

Define content in multiple languages:

```yaml
.localization
  - English:
    - welcome: Welcome
    - goodbye: Goodbye
    - error: Error occurred
  - Italian:
    - welcome: Benvenuto
    - goodbye: Arrivederci
    - error: Si è verificato un errore
  - French:
    - welcome: Bienvenue
    - goodbye: Au revoir
    - error: Une erreur s'est produite
```

### Using Localized Content

```
.locale {welcome}  <!-- Shows "Welcome", "Benvenuto", or "Bienvenue" based on document language -->
```

### Automatic Localization

Many built-in functions automatically localize their content when `doclang` is set:

```
.box type:{tip}
  Content here
  <!-- Title automatically becomes "Tip", "Suggerimento", "Conseil", etc. -->
```

---

This concludes the Quarkdown Technical Reference. For user-friendly guides and tutorials, see the [Quarkdown User Guide](Quarkdown-User-Guide.md).

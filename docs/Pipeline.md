> *This section aims to be a simplification of what is explained in the author's Bachelor's thesis: [Quarkdown - Typesetting versatile di documenti articolati](https://amslaurea.unibo.it/id/eprint/33690/1/garofalo_giorgio_tesi.pdf) (Italian), in which Quarkdown's architecture is thoroughly explained and documented. The thesis is updated to September 2024, while this section is going to be kept up-to-date.*

When an input file is supplied to Quarkdown, it undergoes a process of elaboration to be transformed into an output resource, such as an HTML document that the browser can display. Under the hood, this process is represented by a **sequential pipeline**, in which the output of one stage becomes the input of the next one.

1. [**Lexing**](pipeline%3A-lexing)
2. [**Parsing**](pipeline%3A-parsing)
3. [**Function call expansion**](pipeline%3A-function-call-expansion)
4. [**Tree traversal**](pipeline%3A-tree-traversal)
5. [**Rendering**](pipeline%3A-rendering)
6. [**Post-rendering**](pipeline%3A-post-rendering)
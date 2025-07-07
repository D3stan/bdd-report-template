Iterable values are ordered lists or unordered set that can be iterated through a [loop](loops).

Iterables can also be destructured: see [*Destructuring*](destructuring) for more.

## Collection

An ordered or unordered Markdown list is automatically converted to an ordered collection.

```markdown
.var {letters}
  - A
  - B
  - C

.foreach {.letters}
  .1::lowercase
```
> a
>
> b
>
> c

Nested collections can be represented by nested Markdown lists as well:

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
> A
>
> C
>
> E

## Pair

A pair is an iterable of two values.

It may be created via **`.pair {first} {second}`** or retrieved as a [Dictionary](dictionary) entry.

## Dictionary

When used in a function which requires an iterable, a [Dictionary](dictionary) value is used as a list of key-value pairs.

## Range

An integer [`Range`](range) is a valid ordered iterable value.

# Operations

Assuming `myiterable` to be an iterable, useful operations such as `getat`, `sorted`, `average` and many more can be accessed via [function call chaining](syntax-of-a-function-call#chaining-calls) as `.myiterable::operation`.

For a complete list of operations, please refer to the stdlib's [`Collection` documentation](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Collection).
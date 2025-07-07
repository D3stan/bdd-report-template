The **`.if`** function begins a conditional statement.
1. Its first parameter is the condition ([`Boolean`](boolean)) to satisfy;
2. The second parameter is a parameter-less [lambda](lambda), invoked only if the condition is satisfied.

```
.if {yes}
  Hello, Quarkdown!
```
> Hello, Quarkdown!

The function returns the evaluation of the lambda if the condition is satisfied; nothing otherwise.  
This means the function *propagates* its content up the stack.

```html
<!-- Read this from bottom to top -->

.if {yes} <!-- (nothing) -->
  .if {no} <!-- (nothing) -->
    .if {yes} <!-- Hello! -->
      .if {yes} <!-- Hello! -->
        Hello!
```
> (no output)

This allows the function to be used as part of any expression:

```
.row
  A

  .if {condition}
    B

  C
```

The **`.ifnot`** function is a shorthand that inverts `.if`'s behavior, returning a concrete value only if the condition is *not* satisfied.

The *else* statement is not yet implemented. It could however be emulated thanks to the [`.let`](let) function:

```html
.let {condition}
  .if {.1} <!-- .1 is the implicit lambda argument, equal to let's value -->
    Result if true
  .ifnot {.1}
    Result if false
```
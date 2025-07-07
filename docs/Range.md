The syntax to define a range is **`a..b`**, with `a` and `b` non-negative integers, e.g. `2..10`.

Both `a` and `b` might also be omitted - in that case the range becomes *open*.

According to the amount of delimiters provided, a range can be classified as:

- Closed range: `a..b`
- Open on the left end: `..b`
- Open on the right end: `a..`
- Open on both ends: `..`

The behavior of open ranges is not universally defined, but rather defined by each function that accepts a range: see [`.read`](file-data#file-text-content) as an example, whose strategy is common for slicing operations across the stdlib.

&nbsp;

The `..` operator is syntactic sugar for the **`.range {from} {to}`** function, with the difference that the first accepts only literal values. When the ends of the range need to be evaluated dynamically, such as through a mathematical operation, `.range` is the appropriate choice.
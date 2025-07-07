Boolean values are represented by the following literals (**case insensitive**):

| Boolean value | Literals |
|---------------|----------|
| **`true`**  | `true`, `yes` |
| **`false`** | `false`, `no` |

It is actually encouraged to use the `yes`/`no` literals as they contribute towards the 'natural language flow' of the language.

Example:
```
.code linenumbers:{no}
  My code
```

# Operators

A `Boolean` is returned by the following operator functions:
- `.not {bool}` - [chaining](syntax-of-a-function-call#chaining-calls) is suggested: `.bool::not`
- `.islower {a} {than}`
- `.isgreater {a} {than}`
- `.isequal {a} {to}`
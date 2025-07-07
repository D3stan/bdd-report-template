A **lambda** is a block of code that maps a variable amount of parameters into a single output value of any type (see the *Value types* section of this wiki).

Its syntax is:

```
param1 param2 param3:
My code
```

Where `param1 param2 param3:` is the *header* of the lambda, where parameter names are defined. Their values can be accessed as if you were dealing with [variables](variables):

```
param1 param2 param3:
The second parameter is .param2
```

The header can be omitted:
- If the lambda expects 0 parameters (e.g. [conditional statements](conditional-statements))
- In any other case, the parameters become *implicit* and can be accessed by position via `.1`, `.2`, `.3`, etc.

```
The second parameter is .2
```

Lambdas are the only construct able to fork and create new **scopes**. 
- Nested scopes inherit properties from their parent, such as defined variables and functions;
- Properties defined inside of a nested scope cannot be accessed by their parent, meaning variables defined within a lambda block do not exist outside of the lambda itself.

# Inline lambda
Lambdas are defined the same way, whether they’re in a block or an inline argument (those wrapped in curly braces). However, for inline arguments, an additional **`@lambda`** instruction is required at the beginning, in order to assist the compiler in recognizing it’s dealing with a lambda.

```
.myfunction {@lambda x y: The values are .x and .y}
```

Implicit parameters can be used as well:

```
.myfunction {@lambda The values are .1 and .2}
```

This is only needed if parameters of the lambda are accessed. If the evaluation is constant, `@lambda` can be omitted.

# Examples

### [`.foreach`](loops)

```
.foreach {2..5}
  n:
  The number is **.n**
```

With implicit parameter:

```
.foreach {2..5}
  The number is **.1**
```

### [`.function`](declaring-functions)

`.function`'s body is a lambda that accepts a variable amount of *explicit* parameters:

```
.function {area}
  width height:
  .multiply {width} by:{height}
```

### [`.takeif`](none#operations)

```
.num::takeif {@lambda x: .x::equals {5}}
```
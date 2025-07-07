Functions can also be declared in Quarkdown sources via the **`.function`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Flow/function.html)</sup> function (everything is a function!).

It accepts two arguments: the function name and its body.

```
.function {myfunc}
  Hello, world!
```

It can then be called through a normal function call:

```html
.myfunc <!-- Hello, world! -->
```

Note that there are no return statements: every reached statement is part of the output.

```html
.function {myfunc}
  .if {false}
    A
  B

.myfunc <!-- B -->
```

# Parameters

The body parameter is a [lambda](lambda): each parameter of the function is as a parameter of the lambda block. Each argument can be accessed within the function body as a [variable](variables) (which, in Quarkdown, is basically a function with no parameters).

```html
.function {greet}
  to from:
  Hello, .to from .from!
 
.greet {world} {John} <!-- Hello, world from John! -->
```

Arguments can be named as well to improve readability:

```html
.greet {world} from:{John}
```

Any Markdown content can be returned:

```html
.function {greet}
  to from:
  **Hello, .to** from .from!
```

Quarkdown is [weakly typed](typing) and any kind of value can be returned:

```
.function {area}
  width height:
  .multiply {width} by:{height}

The area of the rectangle is **.area {4} {2}**.
```

```html
.function {isadult}
  age:
  .isgreater {.age} than:{18} orequals:{yes}


.if {.isadult age:{26}}
  You're an adult!
```

## Optional parameters

If a function parameter ends in a question mark `?`, it becomes optional. If the corresponding argument is not provided, it will be assigned the value [`None`](none).

```html
.function {greet}
  to from?:
  Hello, .to from .from!

.greet {world} <!-- Hello, world from None -->

.greet {world} {John} <!-- Hello, world from John -->
```

`None` features several interesting [operations](none#operations), such as placeholders via `.otherwise` which emulate the behavior of default parameters.

```html
.function {greet}
  to from?:
  Hello, .to from .from::otherwise {unnamed}!

.greet {world} <!-- Hello, world from unnamed! -->

.greet {world} {John} <!-- Hello, world from John! -->
```
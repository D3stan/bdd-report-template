Quarkdown is **dynamically typed**: every value that may be passed to a function argument is wrapped in a [`DynamicValue`](https://github.com/iamgio/quarkdown/blob/main/core/src/main/kotlin/eu/iamgio/quarkdown/function/value/DynamicValue.kt) object.

The dynamic value is then *adapted* or converted to the type expected by the signature of the native function (written in Kotlin, strongly typed) at invocation time.  
If a conversion cannot be made, an error occurs.

This invoke-time adaptation reduces constraints, allowing the same value to be handled differently depending on its context.

> ```
> .var {myvar} {true}
>
> .if {.myvar}
>     My value is .uppercase {.myvar}
> ```
> Output:  
> My value is TRUE

In this example:
- `.var`'s second parameter accepts a `DynamicValue` since its value can still be used as any type, thus its value is kept dynamic;
- `.if` takes a [`Boolean`](boolean), so the dynamic `true` value kept in the `myvar` variable is converted to boolean;
- `.uppercase` takes a `String`, so the the `true` value is used as a string.

See the *Value types* section of this wiki to see all the supported types.

## Example: *source + result*

The following example is a simplified version of a function defined in the [demo presentation](https://github.com/iamgio/quarkdown/blob/main/demo/demo.qmd), which shows a Quarkdown code snippet and its visual result right below it:

```html
.function {sourceresult}
  source:
  .code {markdown}
    .source
  .source
```

> Invoking:
> ```markdown
> .sourceresult
>   ## Quarkdown
>   Quarkdown was born in **.sum {2000} {24}**!
> ```

> Output:
> ```markdown
> ## Quarkdown
> Quarkdown was born in **.sum {2000} {24}**!
> ```
> ## Quarkdown
> Quarkdown was born in **2024**!

What this example shows is how versatile Quarkdown values are. In the function declaration, the `.source` argument is retrieved twice:
- In [`.code`](code), which expects a string, so the source is read as-is and inserted in a code block;
- At the top level: the Quarkdown source is automatically adapted to the context, so it's parsed as rich Markdown content.
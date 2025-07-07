**`.var {name} {value}`** defines a variable. `value` is a [dynamic value](typing), meaning it may be of any type.

```
.var {name} {Quarkdown}
```

The variable can be accessed as a parameter-less function:

```
Hello, **.name**!
```
> Hello, **Quarkdown**!

&nbsp;

A variable can be reassigned, either via `.myvar {newvalue}` or `.var {myvar} {newvalue}`:

```html
.var {num} {5}

.num

.num {.sum {.num} {1}}
<!-- Or, equivalently -->
.var {num} {.sum {.num} {1}}

.num
```
> 5
>
> 6

&nbsp;

As mentioned in [Syntax of a function call](syntax-of-a-function-call):
> A body argument always refers to the last parameter of the signature [...]

This allows the variable's value to be either inline or block:

```
.var {myrow}
  .row gap:{2cm}
    A

    B

    C

.container background:{yellow} padding:{1cm}
  .myrow
```
> <img width="600" alt="Result" src="https://github.com/user-attachments/assets/2e6b5cd9-c25c-4806-8170-53e5293dcdf8">

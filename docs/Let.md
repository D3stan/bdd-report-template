The **`.let`** function defines a temporary variable, accessible only within its scope. It accepts two parameters:
1. The value, of [any type](typing), to assign to the scoped variable;
2. A [lambda](lambda) block that accepts one parameter (the given value, indeed)

```
.let {.multiply {4} {2}}
  area:
  The area of the rectangle is .area.
  If it were a triangle, it would have been .divide {.area} by:{2}.
```
> The area of the rectangle is 8.  
> If it were a triangle, it would have been 4.

&nbsp;

The function returns the evaluation of the lambda, thus it can be used as an expression:

```
.center
  .let {Quarkdown}
    name:
    .uppercase {.name}, .lowercase {.name}, .capitalize {.name}
```
> <img width="600" alt="Result" src="https://github.com/user-attachments/assets/ccbe13b2-5d87-47b3-af47-eefcc1507cc1">

&nbsp;

The lambda block accepts implicit positional parameters (see [*lambda*](lambda))
```
.center
  .let {Quarkdown}
    .uppercase {.1}, .lowercase {.1}, .capitalize {.1}
```

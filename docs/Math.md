Mathematical functions provide a way of performing numeric operations.

```
.var {radius} {8}
 
If we try to calculate the **surface** of a circle of **radius .radius**,
we'll find out it's **.pow {.radius} to:{2}::multiply {.pi}::truncate {2}**
```
> If we try to calculate the surface of a circle of **radius 8**, we’ll find out it’s **201.06**

&nbsp;

Handling complex math is particularly effective when used in combination with [function call chaining](syntax-of-a-function-call#chaining-calls). The following two calls are equivalent, with the latter being more natural:

```
.truncate {.multiply {.pow {.radius} to:{2}} by:{.pi}} {2}
```

```
.pow {.radius} to:{2}::multiply {.pi}::truncate {2}
```

&nbsp;

Please refer to stdlib's [`Math` documentation](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Math) for a complete list of available functions.
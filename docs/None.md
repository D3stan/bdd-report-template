*None* is a particular value, which represents nothing or emptiness (similarly to `null` in many programming languages).  
Functions can return it, and it's also used as a placeholder for [optional parameters](declaring-functions#optional-parameters).

# Operations

| Function | Description | Return type |
|-----------|-------------|---------|
| `.none` | Creates an empty value. | `none` |
| `.isnone {value}` | Checks whether `value` is `none`. | [`Boolean`](boolean) |
| `.otherwise {value} {fallback}` | Returns `value` if it is not `none`, `fallback` otherwise.<br/>*Works best with [function call chaining](syntax-of-a-function-call#chaining-calls).* | Type of either `value` or `fallback` |
| `.ifpresent {value} {lambda}` | If `value` is not `none`, maps it to a new value according to the [lambda](function). If `none`, returns `none`.<br/>*Works best with function call chaining.* | Type returned by `lambda`, or `none` |
| `.takeif {value} {lambda}` | Returns `value` if the boolean-returning [lambda](lambda) is accepted on `value`. Returns `none` otherwise.<br/>*Works best with function call chaining.* | Type of `value`, or `none` |

### Examples

```
Hi! I'm .name::otherwise {unnamed}
```
> If `name` is `John`: *Hi! I'm John*  
> If it is `none`: *Hi! I'm unnamed*

&nbsp;

```
.num::takeif {@lambda x: .x::equals {5}}
```
> If `num` is 5: *5*  
> Otherwise: *None*

> Confused about `@lambda`? It begins a parametric [inline `Lambda`](lambda#inline-lambda). Check its page for further details.

&nbsp;

```
.num::takeif {@lambda x: .x::iseven}::ifpresent {Even}::otherwise {Odd}
```
> If `num` is even: *Even*  
> Otherwise: *Odd*

&nbsp;

```
.x::ifpresent {@lambda Yes, .1 is present}::otherwise {Not present}
```
> If `x` is `something`: *Yes, something is present*  
> If it is `none`: *Not present*

> Here, the lambda parameter is implicit and accessed by position.
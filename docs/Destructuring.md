# Destructuring

Destructuring is the operation that splits a [lambda](lambda) parameter into its bare components. For instance, a [pair](iterable#pair) has two components, while a generic [iterable](iterable) has many.

The following types are destructurable:
- [`Iterable`](iterable) (including [`Pair`](iterable#pair))
- [`Dictionary`](dictionary) (as an iterable of pairs)

A value is destructured into `N` components if all the following conditions are met:
- Its type is destructurable;
- The lambda expects a single argument (such as [`.foreach`](loops));
- `N > 1` lambda parameters are supplied.

When the lambda argument is destructured, the operation is performed on its components rather than the element itself.

&nbsp;

# Example: `.foreach`

In the following example we define a [Dictionary](dictionary) and iterate over its destructured key-value components:

```markdown
.var {mydictionary}
  .dictionary 
    - a: 1
    - b: 2
    - c: 3

.foreach {.mydictionary}
    key value: <!-- 2 lambda parameters = each pair is destructured into its 2 components -->
    **.key** has value **.value**
```
> **a** has value **1**
>
> **b** has value **2**
>
> **c** has value **3**

&nbsp;

# Example: `.sorted`

In the following example we define a [Dictionary](dictionary) and iterate over its destructured key-value components via `.foreach` as in the previous example,
but only after sorting its entries by value via [`.sorted`](iterable#operations), which takes a lambda that defines the ordering criteria.

> [!NOTE]
> Remember that `@lambda` is required when declaring an [inline lambda](lambda#inline-lambda).

```markdown
.var {mydictionary}
    .dictionary
        - a: 3
        - b: 1
        - c: 2

.foreach {.mydictionary::sorted by:{@lambda name value: .value}}
   name value:
   .name
```
> b
>
> c
>
> a
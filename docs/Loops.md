# For-each

The main type of loop is provided by the **`.foreach`** function, which accepts:
1. An [`Iterable`](iterable) value;
2. A 1-parameter lambda block, where the argument is the current item being iterated.

```markdown
.foreach {2..4}
  n:
  The number is: **.n**
```
> The number is: **2**
>
> The number is: **3**
>
> The number is: **4**

&nbsp;

The function returns an ordered iterable **collection** of the same size of the input one, containing the evaluation of the lambda for each iterated value.  
Thus, the function can be used as an expression:

```html
.row alignment:{spacearound}
  .foreach {1..3}
    *.1* <!-- .1 is an implicit lambda argument: refers to the first parameter -->
```
> <img width="600" alt="Result 1" src="https://github.com/user-attachments/assets/456e6e61-ec42-498a-86de-7130eae25244">

&nbsp;

Any iterable value is accepted. Here we use a Markdown list:

```markdown
.var {letters}
  - A
  - B
  - C

.foreach {.letters}
  ### .1

  The letter is **.1**.
```
> <img width="600" alt="Result 2" src="https://github.com/user-attachments/assets/cd176eba-1d45-4d7a-aec9-4ec58714dd84">

See [*Iterable*](iterable) for all possible ways of defining an iterable value.

&nbsp;

The type of iterated elements is preserved (see [*Typing*](typing) for more):

```markdown
.row alignment:{spacearound}
  .foreach {1..5}
    n:
    .multiply {.n} by:{.n}
```
> <img width="600" alt="Result 3" src="https://github.com/user-attachments/assets/0f8fd1b2-2fe0-491e-95bf-7f30032319e1">

&nbsp;

# Repeat

The **`.repeat {times}`** function is a shorthand for `.foreach {1..times}`.

```
.repeat {3}
  .1
```
> 1
>
> 2
>
> 3


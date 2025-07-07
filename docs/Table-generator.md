The **`.table`** function takes a single block argument which is an [iterable](iterable) of **tables**.  
The result of the call is a **new table** which is the combination, **by columns** of the supplied tables.

In the following example `.repeat` is used, which, as other supported [loops](loops) do, returns the results from each iteration as an iterable.

```
.table
  .repeat {3}
    n:
    | Column .n |
    |-----------|
    | Cell .n:1 |
    | Cell .n:2 |
    | Cell .n:3 |
```
> <img width="400" alt="Result" src="https://github.com/user-attachments/assets/f4308c8a-084d-432b-be4e-b2a38e095a84">


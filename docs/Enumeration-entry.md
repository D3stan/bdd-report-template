An **enumeration entry** is an input value that matches the name of an element from an enumeration. Enumerations cannot be created from the Quarkdown language, so by *enumeration* we refer to a native JVM `enum`.

This value type is common among function parameters in the stdlib. From the user side, they are just strings. The main difference happens at invocation time, where an error is thrown if the value does not match any of the available entries.

Name matching follows the following rules:
- **Case-insensitive**  
  > `normal` is the same as `NORMAL`
- **Spacing**: words in native entries are separated by an `_` (underscore), which can be - and should be - omitted.  
  > `spacebetween` is the same as `space_between`

&nbsp;

> Examples:
> - [Page format](page-format)
>   ```html
>   .pageformat {A4} <!-- A4 is an entry of PageSizeFormat -->
>   ```
>
> - [Stacks](stacks)
>   ```html
>   .row alignment:{center} <!-- center is an entry of MainAxisAlignment -->
>     ...
>   ```
>
> - [Box](box)
>   ```html
>   .box type:{warning} <!-- warning is an entry of Box.Type -->
>     ...
>   ```
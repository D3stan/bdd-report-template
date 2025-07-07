A block of code can be created as the standard Markdown specification allows, by either a 4-spaces/1-tab indentation or a delimitation of 3 backticks/tildes.

However, Quarkdown also provides a more powerful **`.code`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Text/code.html)</sup> block function, so **what's the difference**?

## `.code` vs. standard code block

### Content processing
- Standard code blocks don't allow any processing of their content, which is instead rendered as-is;
- `.code`'s body parameter accepts any Quarkdown string, making it possible to **evaluate functions** before displaying their output as code.  
  This can be extremely useful when using `.code` in combination with [`.read`](file-data) to load a code snippet from file:
  ```
  .code
    .read {Point.java}
  ```

### Language specification
- Standard fenced code blocks define their language right after the starter delimiter (e.g. ` ```markdown `);
- `.code` elements define their language through the optional `lang` argument (e.g. `.code {markdown}` or `.code lang:{markdown}`)

### Line numbers
- Standard code blocks always show line numbers by default;
- `.code` allows toggling line numbers via the optional `linenumbers` [`Boolean`](boolean) argument, which defaults to `true`.

### Focused lines
`.code` allows focusing a [`Range`](range) of lines (beginning from `1`).  
Line numbers are required to be enabled in order for this to work, due to the internal implementation.

```java
.code {java} focus:{8..10}
   public final class Wrapper<T> {
       private final T value;

       public Wrapper(T value) {
          this.value = value;
       }

       public final T getValue() {
           return this.value;
       }
   }
```

<img width="900" alt="Focused code" src="https://github.com/user-attachments/assets/c9a3a22a-302f-4217-bda9-c38c95caeb65">

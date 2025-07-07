Stack functions are those, in the subcategory of layout functions, that arrange a group of elements according to certain layout rules. There are three of them: 
- **`.row`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Layout/row.html)</sup>
- **`.column`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Layout/column.html)</sup>
- **`.grid`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Layout/grid.html)</sup>

---

In order to understand which elements they must handle, they rely on the strict Markdown concept of block, an isolated chunk of the document such as a paragraph, a code block, a list, a quote, etc.

```
.row
  A

  B

  C
```

The following example has only one item, as both A, B and C are part of the same paragraph (due to *lazy lines*):

```
.row
  A
  B
  C
```

Images are stackable too, as long as they are in different paragraphs.

```
.row
  ![](img1.png)

  ![](img2.png)
```

Every kind of block is supported:

~~~
.row
  > This is
  > a quote

  ```java
  This is code
  ```

  - This is
  - a list
~~~

According to the CommonMark specification, the following example brings to the same result as the previous one. It's however encouraged to keep the code well readable by spacing blocks properly.

~~~
.row
  > This is
  > a quote
  ```java
  This is code
  ```
  - This is
  - a list
~~~

All the stack functions accept the following optional arguments:

| Parameter | Description | Accepts |
|-----------|-------------|---------|
| `alignment` | Main axis alignment (CSS' `justify-content`). | `start`, `center`, `end`, `spacebetween`, `spacearound`, `spaceevenly` |
| `cross` | Cross axis alignment (CSS' `align-items`). | `start`, `center`, `end`, `stretch` |
| `gap` | Space between items. | [`Size`](sizes) |

`grid` also accepts a mandatory `columns` argument, which takes an integer value.

```
.grid columns:{2} alignment:{spacearound} gap:{1cm}
  A

  *B*

  **C**

  ***D***
```

<img width="600" alt="Grid result" src="https://github.com/user-attachments/assets/2bd5b3f3-5c28-4996-b31e-374efa2d3fb5">

Other elements can join too:

```
# Contacts

.row alignment:{spacearound}
  .center
    **Michael Scott**  
    Dunder Mifflin Paper Company, Inc.    
    [michaelscott@example.com](mailto:michaelscott@example.com)

  .center
    **Forrest Gump**  
    Bubba Gump Shrimp Co.  
    [forrestgump@example.com](mailto:forrestgump@example.com)
```

<img width="600" alt="Contacts example" src="https://github.com/user-attachments/assets/d227dcc7-d12b-48f7-b634-8fff4f338080">


Stack layouts can be infinitely nested within each other:

```
.row cross:{center} gap:{1in}
  A

  .grid columns:{2}
    B

    C

    D

    E

  .column gap:{5mm}
    F
  
    .row
      G

      H
```

<img width="600" alt="Nested stacks" src="https://github.com/user-attachments/assets/7c224f39-86a3-4823-bde8-c6e684dac6e5">


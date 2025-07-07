The **`.collapse`** function creates an interactive collapsible block, whose status can be toggled by clicking.

It requires an [inline](markdown-content#inline-content) title (always displayed) and [block](markdown-content#block-content) content (displayed when expanded).

```markdown
.collapse {A _collapsible_ block. **Click me!**}
  Hidden content...  
  **Surprise!**

  .loremipsum
```

> Collapsed:  
> <img width="600" alt="Collapsed" src="https://github.com/user-attachments/assets/09b88a07-fbd2-4f41-9867-e3957b2f0626">
>
> Expanded:  
> <img width="600" alt="Expanded" src="https://github.com/user-attachments/assets/710100b5-a4fa-4697-b99e-4c5d9cd73e41">

&nbsp;

The initial status of a block can be changed via the optional `open` [`Boolean`](boolean) argument, which defaults to `false` (collapsed).

```markdown
.collapse {A _collapsible_ block. **Click me!**} open:{yes}
  ...
```


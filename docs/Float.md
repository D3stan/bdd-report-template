The **`.float {alignment}`** function can turn any content into a floating element, breaking the normal flow and allowing subsequent content to wrap around it.

`alignment` accepts `start` or `end`.


```
.float {start}
    !(80%)[Quarkdown](icon.png)

.loremipsum
```

<img width="600" alt="Floating image" src="https://github.com/user-attachments/assets/816e20f5-ecf9-4dae-9f89-726270f6e001" />

&nbsp;

Along with images, any other content can become floating:

```
.float {end}
    .box {Hello} type:{warning}
        Floating!

.loremipsum
```

<img width="600" alt="Floating box" src="https://github.com/user-attachments/assets/e3921535-4b0a-4a1f-a041-f8d75646567e" />


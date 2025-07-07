The **`.clip {shape}`** block function allows clipping its content to a defined shape.

Supported shapes:
- `circle`

```markdown
![Sky](sky.jpg)

.clip {circle}
    ![Sky](sky.jpg)
```

<img width="600" alt="Circle sky" src="https://github.com/user-attachments/assets/f49dcb96-2e68-4cf7-94fd-71adad0072c7" />

&nbsp;

In case of a [figure](image-figure) only the content is affected, leaving its caption intact:

```markdown
![Sky](sky.jpg "A beautiful sky.")

.clip {circle}
    ![Sky](sky.jpg "A beautiful sky.")
```

<img width="600" alt="Circle sky figure" src="https://github.com/user-attachments/assets/29b84532-d517-4857-a3c9-a70dfbea5a78" />

&nbsp;

Not just images — clipping works with any content. Here a [container](container) is used:

```markdown
.clip {circle}
    .container padding:{2cm} background:{orange}
        #! Hello!
```

<img width="400" alt="Circle container" src="https://github.com/user-attachments/assets/ce1f0bd8-76de-4dce-863f-0aff4644d77a" />

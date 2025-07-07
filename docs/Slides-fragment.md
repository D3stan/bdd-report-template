A **fragment** is an interactive section of a slide which may show or hide content when the user attempts to go to the next slide.

A fragment can be created via the **`.fragment`** block function, which takes the content as a body argument, and also accepts an optional `behavior` argument which can take any of the following:

| Behavior name | Description |
|---------------|-------------|
| **`show`** (default) | Starts invisible, fades in on interaction. |
| **`hide`** | Starts visible, fades out on interaction. |
| **`semihide`** | Starts visible, fade out to 50% on interaction. |
| **`showhide`** | Starts invisible, fades in on interaction, then out on the next interaction. |

If multiple fragments are present within the same slide, they are triggered in order.
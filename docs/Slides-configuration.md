The **`.slides`**<sup>[[docs]](https://quarkdown.com/docs/quarkdown-stdlib/com.quarkdown.stdlib.module.Slides/slides.html)</sup> function allows overriding the default configuration of `slides` documents. All its parameters are **optional**, and are:

| Parameter | Description | Accepts | Default |
|-----------|-------------|---------|---------|
| `center` | Whether content should be centered vertically. | [`Boolean`](boolean) | Up to the current layout theme. |
| `controls` | Whether navigation controls should be shown. | [`Boolean`](boolean) | `true` |
| `transition` | Transition style between slides. | `none`, `fade`, `slide`, `zoom` | `slide` |
| `speed` | Transition speed between slides.<br/>Requires `transition` to be set. | `default`, `fast`, `slow` | `default` |
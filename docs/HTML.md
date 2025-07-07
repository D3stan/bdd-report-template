Standard Markdown specifications allow freely mixing Markdown and HTML, as they're meant to be implemented by parsers that solely rely on HTML rendering.

```markdown
**Hello** <em>world</em>!
```

On the other hand, Quarkdown strongly encourages **target agnosticism**, in order to maintain rendering consistency across all supported rendering target.

At this time, only HTML rendering is supported (note: PDF export is not a rendering target, as it works on top of HTML post-processing).
There are however future plans to bring support to more targets, such as LaTeX. In that case, HTML content can't be handled by the native target anymore.

For this reason, Quarkdown dropped mixed content support, and focused on covering the most frequent HTML workarounds with dedicated functions, for instance:

- A collapsible block in standard Markdown via HTML:
  ```markdown
  <details>
  <summary>Title of the collapsible block</summary>
  Content of the collapsible block.
  </details>
  ```
- The same in Quarkdown, using the [`.collapse`](collapsible) function:
  ```
  .collapse {Title of the collapsible block}
    Content of the collapsible block.
  ```

# Forcing HTML injection

As a last resort, if the functionality you're looking for is not supported out of the box, you might consider calling the `.html` function, which directly renders its content into the final document, as long as the rendering target is HTML.

```markdown
**Hello** .html {<em>world</em>}!
```

```markdown
.html
  <div class="my-container">
    My HTML container
  </div>
```

> [!WARNING]
> - The rendered output is unsanitized content, possibly vulnerable.
> - This approach is not target-agnostic, as other rendering targets will ignore the provided content.
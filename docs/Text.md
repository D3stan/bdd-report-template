The **`.text`** inline function provides extensive text formatting that cannot be expressed in plain Markdown.

| Parameter | Accepts |
|-----------|---------|
| **`text`** (mandatory) | Inline content. |
| **`size`** | `tiny` (50%), `small` (75%), `normal` (100%), `medium` (125%), `larger` (150%), `large` (200%), `huge` (300%) |
| **`weight`** | `normal`, `bold` |
| **`style`** | `normal`, `italic` |
| **`decoration`** | `underline`, `overline`, `underoverline`, `strikethrough`, `all` |
| **`case`** | `uppercase`, `lowercase`, `capitalize` |
| **`variant`** | `normal`, `smallcaps` |
| **`url`** | URL to link to. If set, the text becomes a link. If the URL is set but empty, the URL is the text content (assuming it represents a valid URL). |

```markdown
# A demo of .text {Quarkdown} variant:{smallcaps}

Lorem .text {ipsum} size:{large} decoration:{underoverline} dolor sit amet
```
> <img width="450" alt="Result" src="https://github.com/user-attachments/assets/0c290098-11b3-4ea7-b874-96eea2489870">

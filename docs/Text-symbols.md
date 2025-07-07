Quarkdown features automatic text replacement for commonly used UTF-8 symbols.

Text is automatically replaced wherever inline content is accepted (e.g. paragraphs, blockquotes, boxes, ... - NOT code blocks/spans, math, URLs, ...).

| Syntax | Rendered | Conditions                                                                                    |
|--------|----------|-----------------------------------------------------------------------------------------------|
| -      | —        | Preceded by a word character and a whitespace, followed by a whitespace and a word character. |
| ...    | …        | Either at the beginning or end of a word, not in-between.                                     |
| ->     | →        |                                                                                               |
| <-     | ←        |                                                                                               |
| =>     | ⇒        |                                                                                               |
| <==    | ⇐        |                                                                                               |
| >=     | ≥        |                                                                                               |
| <=     | ≤        |                                                                                               |
| !=     | ≠        |                                                                                               |
| +-     | ±        |                                                                                               |
| '      | ‘        | Not preceded by a word character, followed by a word character.                               |
| '      | ’        | Not preceded by a whitespace.                                                                 |
| "      | “        | Not preceded by a word character, followed by a word character.                               |
| "      | ”        | Not preceded by a whitespace, not followed by a word character.                               |
| (C)    | ©        |                                                                                               |
| (R)    | ®        |                                                                                               |
| (TM)   | ™        |                                                                                               |


Escaping a sequence with a backslash `\` will prevent the text from being replaced: 
```
\->
```
Quarkdown offers full Mermaid interoperability via the **`.mermaid`** block function, bringing Mermaid diagrams and charts into your documents.

Its block parameter accepts the Mermaid code content. Please refer to [Mermaid's documentation](https://mermaid.js.org/intro/) for information about its powerful syntax to create flowcharts, pie charts, class and sequence diagrams, and many more. 

```
.mermaid
  flowchart TD
    A([Start]) --> B[Enter username and password]
    B --> C{Correct?}
    C -- Yes --> D[Redirect to dashboard]
    C -- No --> E[Show error message]
    D --> F([End])
    E --> F
```

<img width="600" alt="Diagram" src="https://github.com/user-attachments/assets/be366982-011c-48ff-b10b-3813ad997b2b" />

&nbsp;

The Mermaid code accepts Quarkdown function calls:

```
.mermaid
  flowchart TD
    A([Start]) --> B{.n1 + .n2 = ?}
    B -- .sum {.n1} {.n2} --> C([Correct])
```

<img width="600" alt="Diagram with function calls" src="https://github.com/user-attachments/assets/173a45a2-f6d3-41c5-9375-a402e59fb78c" />

&nbsp;

# Diagram from file

Since function calls can be used inside the block argument, the [**`.read`**](file-data) function can be used as well to load text from file.

```
.mermaid
  .read {chart.mmd}
```

# Diagram caption & numbering

An optional `caption` argument assigns a caption to the diagram, and lets the block be numbered according to the document's *figure* [numbering](numbering):

```
.mermaid caption:{My Mermaid diagram.}
  flowchart TD
    A([Start]) --> B[Enter username and password]
    B --> C{Correct?}
    C -- Yes --> D[Redirect to dashboard]
    C -- No --> E[Show error message]
    D --> F([End])
    E --> F
```

<img width="600" alt="Diagram with caption" src="https://github.com/user-attachments/assets/f2487aba-96f7-4e76-ac55-e01f04c5736f" />

&nbsp;

To number the diagram without a caption, pass an empty string as an argument:

```
.mermaid caption:{}
  flowchart TD
    A([Start]) --> B[Enter username and password]
    B --> C{Correct?}
    C -- Yes --> D[Redirect to dashboard]
    C -- No --> E[Show error message]
    D --> F([End])
    E --> F
```

<img width="600" alt="Diagram with empty caption" src="https://github.com/user-attachments/assets/6e94cc87-2067-4b13-ae74-59129543a881" />
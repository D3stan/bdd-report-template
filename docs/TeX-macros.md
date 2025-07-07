When writing [TeX formulas](tex-formulas), it may come in handy to have access to user-defined macros.

The **`.texmacro {name} {content}`** function defines a new macro which can be used in *math* elements.

```latex
.texmacro {\gradient} {\nabla}

$ \gradient f $
```

As with every Quarkdown function, the last argument can be used as a [*block argument*](syntax-of-a-function-call#block-vs-inline-function-calls).

```latex
.texmacro {\gradient}
    \nabla
```

<img width="500" alt="Gradient" src="https://github.com/user-attachments/assets/60bf078b-2d71-42c6-953e-d171acb048c8" />

&nbsp;

# Parameters

Macros can feature a variable number of parameters:

```latex
.texmacro {\sumlim}
    \sum_{#1}^{#2}

$ \sumlim{i=1}{n} a_i $
```

<img width="500" alt="Sum with limits" src="https://github.com/user-attachments/assets/09a2cd3a-8436-4e16-b504-27a42dce3f82" />

&nbsp;

# Composing

Multiple macros can be defined and can be combined, as you would do in LaTeX:

```latex
.texmacro {\hello}
    \text {Hello, \textit {world}}

.texmacro {\highlight}
    \colorbox{yellow}{#1}

$ \highlight{\hello} $
```

And also composed with other macros:

```latex
.texmacro {\hello}
    \text {Hello, \textit {world}}

.texmacro {\highlighthello}
    \colorbox{yellow}{\hello}

$ \highlighthello $
```

<img width="500" alt="Highlighted hello world" src="https://github.com/user-attachments/assets/255f119f-1218-4eae-a31d-0e78d044e936" />

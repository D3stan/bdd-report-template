The built-in [`paper`](https://github.com/iamgio/quarkdown/blob/main/libs/src/main/resources/paper.qmd) library is written in Quarkdown and adds support to typical elements of scientific papers in a LaTeX fashion.

The library features the following components:
- Abstract
- Titled, numbered blocks:
  - Definitions
  - Lemmas
  - Theorems
  - Proofs

> [!NOTE]
> The supported languages are aligned to the ones supported by Quarkdown's core: currently English and Italian. See [*Built-in localization*](localization#built-in-localization) for further information.

&nbsp;

The first step is to [import](importing-external-libraries) the library:
```
.include {paper}
```

## Abstract

**`.abstract`** can generate the layout for a titled *abstract* block. Its content goes in its block argument:

```markdown
.abstract
    This is my *abstract*! Here goes the summary of the document.  
    .loremipsum

This is not part of the abstract, instead.
```

<img width="630" alt="Abstract" src="https://github.com/user-attachments/assets/d5dbaf26-c253-411a-ae3c-8118726b1bd0" />

&nbsp;

The alignment of the title defaults to center and can be changed via `.abstractalignment {start|center|end}`:

```markdown
.abstractalignment {start}

.abstract
    This is my *abstract*! Here goes the summary of the document.  
    .loremipsum
```

<img width="630" alt="image" src="https://github.com/user-attachments/assets/f6ead1e3-b121-4d3a-ae5b-509b0772a588" />

&nbsp;

## Titled blocks

Any of the following blocks can be created:
- Definition via **`.definition`**
- Lemma via **`.lemma`**
- Theorem via **`.theorem`**
- Proof via **`.proof`**

All the mentioned functions take one block argument which defines the content:

```latex
.definition
    Let $ \Delta x $ be an object's change in position over a time interval $ \Delta t $,
    then the average velocity is defined as $ v = \frac {\Delta x} {\Delta t} $.
```

<img width="600" alt="Definition" src="https://github.com/user-attachments/assets/d212dde3-535e-4982-b48e-9cce676b4eb8" />

&nbsp;

The default title suffix is `.` (dot) and can be customized via `.paperblocksuffix {suffix}`:

```
.paperblocksuffix {:}
```

<img width="600" alt="Custom block suffix" src="https://github.com/user-attachments/assets/93c0108e-fd63-4e8a-80d0-a4fe70c679eb" />

&nbsp;

Defining a [numbering format](numbering) results in the blocks of that type to be numbered.  
The format names are plural: `definitions`, `lemmas`, `theorems`, `proofs`.

```
.numbering
    - definitions: 1.a
    - lemmas: i

...

.definition
    .loremipsum

.lemma
    .loremipsum

.definition
    .loremipsum
```

<img width="600" alt="Numbered blocks" src="https://github.com/user-attachments/assets/ec5982de-fa69-45d0-8bf1-fe2664c8c6f6" />

&nbsp;

Proofs also feature a special *end-of-proof* character, which defaults to `∎`.

```
.theorem
    .loremipsum

.proof
    .loremipsum
```

<img width="600" alt="Proof" src="https://github.com/user-attachments/assets/ece4f874-1d51-443f-808d-e570303f5dd0" />

The end-of-proof can be customized via `.proofend {string}`:

```
.proofend {😎}
```

<img width="600" alt="Proof character customization" src="https://github.com/user-attachments/assets/a48fe7db-7301-4539-88f7-ef49bf3f0b93" />


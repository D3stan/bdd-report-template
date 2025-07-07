Quarkdown natively supports TeX math equations and formulas. When rendering to HTML, this feature is powered by [KaTeX](https://www.katex.org).


# Inline

Inline formulas can be created by wrapping text between two `$` symbols. Both delimiters must be preceded and followed by a whitespace (or beginning/end of the line).

```latex
Let $ \overline v = \frac {\Delta x} {\Delta t} $ be the **average velocity** of an object.
```
> <img width="450" alt="Inline result" src="https://github.com/user-attachments/assets/953f537f-7fd4-4ab8-85f1-7c6d87f701fb">


&nbsp;

# One-line block

Block formulas are usually visually centered and share the same syntax as the inline ones, but need to be isolated from other content:

```latex
The following function is a **Fourier Transform**:

$ F(u) = \int^{+\infty}_{-\infty} f(x) e^{-i 2\pi x} dx $
```
> <img width="750" alt="One-line block result" src="https://github.com/user-attachments/assets/05005da4-53d8-4c2d-87e2-7f82064c1d20">

> [!NOTE]
> This syntax does **not** interrupt paragraphs, so make sure to space blocks properly. If the paragraph is not interrupted, the formula is recognized as inline, due to Markdown's *lazy lines*:
>
> ```latex
> The following function is a **Fourier Transform**:
> $ F(u) = \int^{+\infty}_{-\infty} f(x) e^{-i 2\pi x} dx $
> ```
>> <img width="750" alt="Invalid one-line block" src="https://github.com/user-attachments/assets/e8d4e8d6-69b1-4083-8ded-68e399d8344f">

&nbsp;

# Multiline block

A block formula can span over multiple lines thanks to a syntax similar to fenced code blocks, though using three `$` symbols as delimiters:

```latex
$$$
f(x) =
\begin{cases}
    0 & \text{if } x = 0 \\
    1 & \text{if } x \neq 0
\end{cases}
$$$
```
> <img width="750" alt="Multiline block result" src="https://github.com/user-attachments/assets/c282aff0-19f0-41ae-ab71-41b6f7865710">

&nbsp;

# Macros

Quarkdown supports the creation of TeX macros via the `.texmacro` function. See [*TeX macros*](tex-macros) for more information.
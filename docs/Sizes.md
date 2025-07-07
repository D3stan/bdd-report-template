Many functions accept sizes as arguments. This page explains the correct format to define them.

# Single size (`Size`)

When a **`Size`** value is required, strings with a **numeric value** (either integer or floating point) and a **unit** suffix are accepted.

Supported units:
- `px` pixels;
- `pt` points;
- `cm` centimeters;
- `mm` millimeters;
- `in` inches;
- `%` percentage (relative to parent).

Examples of accepted values are: `12px`, `2cm`, `5.3in`, `30%`.

Units can be omitted. In that case, `px` is used.

# Size group (`Sizes`)

Some other parameters require a group of sizes, also known as **`Sizes`**.  
This is required, for example, by [`.pageformat`](page-format)'s `margin` parameter, and allows setting up to four different values for each side of a rectangle.

Its format is the same as CSS, with three different ways to express a size group:
- **Single value:** a single [`Size`](#single-size-size) value applied to all sides (e.g. `8px`);
- **Vertical/horizontal:** two [`Size`](#single-size-size) values, separated by a space, applied to top-bottom and left-right, respectively (e.g. `2cm 15mm`);
- **TRBL**: four [`Size`](#single-size-size) values, separated by a space, respectively assigned to top, right, bottom and left sides (e.g. `2.1in 4cm 2px 2cm`).
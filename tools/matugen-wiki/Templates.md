# Templates
## Basic Syntax

| Type | Syntax | Description |
|------|---------|-------------|
| **Expression** (Keyword) | `{{ expression }}` | Evaluates and outputs a value. |
| **Block** | `<* ... *>` | Used for loops, conditionals and includes. |
| **Escaping** | `\{{ ... }}` | Escapes template output so it isn’t evaluated. |

---

## Expressions
Use **dot notation** to access nested values inside context objects.

```text
{{ colors.primary.default.hex }}
{{ palettes.error._99.hex }}
{{ mode }}
```

For example:
```
{{ custom.red_color.hex }} -> #ff0000
{{ custom.red_color.rgb }} -> rgb(255, 0, 0)
```

In JSON:
```json
{
  "custom": {
    "red_color": {
      "color": "#ff0000"
    }
  }
}
```

---

## Includes

```text
<* include "filename" *>
```

Includes another template file, the name should be the template name you put in the config.

If you just want to use the included template inside of another one and don't want to write it to a file, you can just comment out the `output_path`
```toml
[templates.includeme]
input_path = "./include.txt"
# The output path is optional if you just want to import the template anyways,
# output_path = "./a/include.txt"
```

**Example:**
```text
<* include "includeme" *>
```

---

## Conditionals

Conditionals allow branching logic inside templates.

```text
<* if {{ condition }} *>
  ...content if true...
<* else *>
  ...content if false...
<* endif *>
```

**Example:**
```text
<* if {{ is_dark_mode }} *>
  Dark Mode
<* else *>
  Light Mode
<* endif *>
```

---

## Loops

### Range Loop
Iterates over a numeric range (inclusive).

```text
<* for i in -10..10 *>
  {{ i }}
<* endfor *>
```

### Key-Value Loop
Iterates through maps or objects, exposing both key and value bindings.

```text
<* for name, value in colors *>
  {{ name }}: {{ value.default.hex }};
<* endfor *>
```

---

## Filters

Filters transform or modify values.  
They are chained using the pipe symbol (`|`).
They can support Expressions as arguments.

**Example:**
```text
{{ colors.primary.default.hex | lighten: 20.0 | invert }}
```

```
<* for i in -10..10 *>
    actual: {{ i }} multiplied: {{ {{ i }} * 10 }} {{ colors.red.default.hex | lighten: {{i}} * 10 }}
<* endfor *>
```

---

## Arithmetic and Nested Expressions

Expressions can be nested or contain arithmetic operations.

```text
{{ {{ i }} * 10 }}
{{ colors.red.default.hex | lighten: {{ i }} * 10 }}
```

---

## Escaping Output

To render raw `{{ ... }}` text without evaluating it:

```text
\{{ colors.primary.default.hex }}
```

This will output literally `{{ colors.primary.default.hex }}` in the result.

---
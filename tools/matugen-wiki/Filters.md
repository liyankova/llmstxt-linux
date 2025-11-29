# Filters


## Color manipulation **(RGBA AND HSLA ONLY)**
<details><summary>Click to expand</summary>

## `set_alpha`

```
{{ colors.source_color.default.rgba | set_alpha: 0.5 }}
```

## `set_hue`

- Only for hsla

```
{{ colors.source_color.default.rgba | set_hue: -180.0 }}
{{ colors.source_color.default.rgba | set_hue: 90.0 }}
```

</p>
</details>

## Color manipulation

<details><summary>Click to expand</summary>

## `grayscale`

```
{{ colors.source_color.default.rgba | grayscale }}
```

## `invert`

```
{{ colors.source_color.default.rgba | invert }}
```

## `set_lightness`
- Increases/Decreases lightness of the provided color
- Can be used on normal strings and color keywords too
- Automatically gets the format from the string and outputs it as the same one

```
{{ "#ffbf9b" | set_lightness: 10.0}}
{{ "rgb(255,255,255)" | set_lightness: 10.0}}

{{ colors.source_color.default.rgb | set_lightness: 20.0 }}
{{ colors.source_color.default.rgb | set_lightness: -20.0 }}
```

## `auto_lightness`
- #ff0000 as hex color input gives 
    - (light to dark)
      - `{{ colors.primary_container.default.hex }}` - **`#ffdad4`**
      - `{{ colors.primary_container.default.hex | auto_lightness: 20.0 }}` - **`#ff826e`**
    - (dark to light)
      - `{{ colors.primary_container.default.hex }}` - **`#73342a`**
      - `{{ colors.primary_container.default.hex | auto_lightness: 20.0 }}` - **`#bc5747`**


</p>
</details>

## String manipulation

<details><summary>Click to expand</summary>

## `camel_case`
- Example:
  - primary_container -> primaryContainer
  - secondary_container -> secondaryContainer

```
<* for name, value in colors *>
${{name | camel_case}}: {{value.default.hex}};
<* endfor *>
```

## `replace`

- This will replace `_` with `-` for every color.
- For example: `surface_dim` -> `surface-dim`.

```
{{ "foo" | replace: "foo", "bar" }}
```

```
<* for name, value in colors *>
    {{name | replace: "_", "-" }} {{value.default.hex}};
<* endfor *>
```

## `to_lower`

```
{{ "TEST" | to_lower }}
```

## `to_upper`

```
{{ "test" | to_upper }}
```

</p>
</details>
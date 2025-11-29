---
source_url: "https://tailwindcss.com/docs/padding"
title: "padding - Spacing - Tailwind CSS"
crawl_date: "2025-11-29T13:36:26.907365Z"
selector: ".isolate .mx-auto"
---

# padding - Spacing - Tailwind CSS

Spacing

# padding

Utilities for controlling an element's padding.

| Class | Styles |
| --- | --- |
| `p-<number>` | `padding: calc(var(--spacing) * <number>);` |
| `p-px` | `padding: 1px;` |
| `p-(<custom-property>)` | `padding: var(<custom-property>);` |
| `p-[<value>]` | `padding: <value>;` |
| `px-<number>` | `padding-inline: calc(var(--spacing) * <number>);` |
| `px-px` | `padding-inline: 1px;` |
| `px-(<custom-property>)` | `padding-inline: var(<custom-property>);` |
| `px-[<value>]` | `padding-inline: <value>;` |
| `py-<number>` | `padding-block: calc(var(--spacing) * <number>);` |
| `py-px` | `padding-block: 1px;` |

Show more

## [Examples](#examples)

### [Basic example](#basic-example)

Use `p-<number>` utilities like `p-4` and `p-8` to control the padding on all sides of an element:

p-8

```
<div class="p-8 ...">p-8</div>
```

### [Adding padding to one side](#adding-padding-to-one-side)

Use `pt-<number>`, `pr-<number>`, `pb-<number>`, and `pl-<number>` utilities like `pt-6` and `pr-4` to control the padding on one side of an element:

pt-6

pr-4

pb-8

pl-2

```
<div class="pt-6 ...">pt-6</div><div class="pr-4 ...">pr-4</div><div class="pb-8 ...">pb-8</div><div class="pl-2 ...">pl-2</div>
```

### [Adding horizontal padding](#adding-horizontal-padding)

Use `px-<number>` utilities like `px-4` and `px-8` to control the horizontal padding of an element:

px-8

```
<div class="px-8 ...">px-8</div>
```

### [Adding vertical padding](#adding-vertical-padding)

Use `py-<number>` utilities like `py-4` and `py-8` to control the vertical padding of an element:

py-8

```
<div class="py-8 ...">py-8</div>
```

### [Using logical properties](#using-logical-properties)

Use `ps-<number>` or `pe-<number>` utilities like `ps-4` and `pe-8` to set the `padding-inline-start` and `padding-inline-end` logical properties, which map to either the left or right side based on the text direction:

Left-to-right

ps-8

pe-8

Right-to-left

ps-8

pe-8

```
<div>  <div dir="ltr">    <div class="ps-8 ...">ps-8</div>    <div class="pe-8 ...">pe-8</div>  </div>  <div dir="rtl">    <div class="ps-8 ...">ps-8</div>    <div class="pe-8 ...">pe-8</div>  </div></div>
```

For more control, you can also use the [LTR and RTL modifiers](/docs/hover-focus-and-other-states#rtl-support) to conditionally apply specific styles depending on the current text direction.

### [Using a custom value](#using-a-custom-value)

Use utilities like `p-[<value>]`,`px-[<value>]`, and `pb-[<value>]` to set the padding based on a completely custom value:

```
<div class="p-[5px] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `p-(<custom-property>)` syntax:

```
<div class="p-(--my-padding) ...">  <!-- ... --></div>
```

This is just a shorthand for `p-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](#responsive-design)

Prefix a `padding` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="py-4 md:py-8 ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](/docs/hover-focus-and-other-states).

## [Customizing your theme](#customizing-your-theme)

The `p-<number>`,`px-<number>`,`py-<number>`,`ps-<number>`,`pe-<number>`,`pt-<number>`,`pr-<number>`,`pb-<number>`, and `pl-<number>` utilities are driven by the `--spacing` theme variable, which can be customized in your own theme:

```
@theme {  --spacing: 1px; }
```

Learn more about customizing the spacing scale in the [theme variable documentation](/docs/theme).

### On this page

* [Quick reference](#quick-reference)
* [Examples](#examples)
  + [Basic example](#basic-example)
  + [Adding padding to one side](#adding-padding-to-one-side)
  + [Adding horizontal padding](#adding-horizontal-padding)
  + [Adding vertical padding](#adding-vertical-padding)
  + [Using logical properties](#using-logical-properties)
  + [Using a custom value](#using-a-custom-value)
  + [Responsive design](#responsive-design)
* [Customizing your theme](#customizing-your-theme)
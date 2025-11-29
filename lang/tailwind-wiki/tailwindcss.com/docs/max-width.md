---
source_url: "https://tailwindcss.com/docs/max-width"
title: "max-width - Sizing - Tailwind CSS"
crawl_date: "2025-11-29T13:36:41.758796Z"
selector: ".isolate .mx-auto"
---

# max-width - Sizing - Tailwind CSS

Sizing

# max-width

Utilities for setting the maximum width of an element.

| Class | Styles |
| --- | --- |
| `max-w-<number>` | `max-width: calc(var(--spacing) * <number>);` |
| `max-w-<fraction>` | `max-width: calc(<fraction> * 100%);` |
| `max-w-3xs` | `max-width: var(--container-3xs); /* 16rem (256px) */` |
| `max-w-2xs` | `max-width: var(--container-2xs); /* 18rem (288px) */` |
| `max-w-xs` | `max-width: var(--container-xs); /* 20rem (320px) */` |
| `max-w-sm` | `max-width: var(--container-sm); /* 24rem (384px) */` |
| `max-w-md` | `max-width: var(--container-md); /* 28rem (448px) */` |
| `max-w-lg` | `max-width: var(--container-lg); /* 32rem (512px) */` |
| `max-w-xl` | `max-width: var(--container-xl); /* 36rem (576px) */` |
| `max-w-2xl` | `max-width: var(--container-2xl); /* 42rem (672px) */` |

Show more

## [Examples](#examples)

### [Basic example](#basic-example)

Use `max-w-<number>` utilities like `max-w-24` and `max-w-64` to set an element to a fixed maximum width based on the spacing scale:

Resize the example to see the expected behavior

max-w-96

max-w-80

max-w-64

max-w-48

max-w-40

max-w-32

max-w-24

```
<div class="w-full max-w-96 ...">max-w-96</div><div class="w-full max-w-80 ...">max-w-80</div><div class="w-full max-w-64 ...">max-w-64</div><div class="w-full max-w-48 ...">max-w-48</div><div class="w-full max-w-40 ...">max-w-40</div><div class="w-full max-w-32 ...">max-w-32</div><div class="w-full max-w-24 ...">max-w-24</div>
```

### [Using a percentage](#using-a-percentage)

Use `max-w-full` or `max-w-<fraction>` utilities like `max-w-1/2` and `max-w-2/5` to give an element a percentage-based maximum width:

Resize the example to see the expected behavior

max-w-9/10

max-w-3/4

max-w-1/2

max-w-1/3

```
<div class="w-full max-w-9/10 ...">max-w-9/10</div><div class="w-full max-w-3/4 ...">max-w-3/4</div><div class="w-full max-w-1/2 ...">max-w-1/2</div><div class="w-full max-w-1/3 ...">max-w-1/3</div>
```

### [Using the container scale](#using-the-container-scale)

Use utilities like `max-w-sm` and `max-w-xl` to set an element to a fixed maximum width based on the container scale:

Resize the example to see the expected behavior

![](https://images.unsplash.com/photo-1501196354995-cbb51c65aaea?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=facearea&facepad=4&w=256&h=256&q=80)

Andrew Alfred

Assistant to the Traveling Secretary

```
<div class="max-w-md ...">  <!-- ... --></div>
```

### [Using breakpoints container](#using-breakpoints-container)

Use the `container` utility to set the maximum width of an element to match the `min-width` of the current breakpoint. This is useful if you'd prefer to design for a fixed set of screen sizes instead of trying to accommodate a fully fluid viewport:

```
<div class="container">  <!-- ... --></div>
```

Note that unlike containers you might have used in other frameworks, Tailwind's container does not center itself automatically and does not have any built-in horizontal padding. Use `mx-auto` and the `px-<number>` utilities to add these:

```
<div class="container mx-auto px-4">  <!-- ... --></div>
```

### [Using a custom value](#using-a-custom-value)

Use the `max-w-[<value>]` syntax to set the maximum width based on a completely custom value:

```
<div class="max-w-[220px] ...">  <!-- ... --></div>
```

For CSS variables, you can also use the `max-w-(<custom-property>)` syntax:

```
<div class="max-w-(--my-max-width) ...">  <!-- ... --></div>
```

This is just a shorthand for `max-w-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](#responsive-design)

Prefix a `max-width` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="max-w-sm md:max-w-lg ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](/docs/hover-focus-and-other-states).

## [Customizing your theme](#customizing-your-theme)

The `max-w-<number>` utilities are driven by the `--spacing` theme variable, which can be customized in your own theme:

```
@theme {  --spacing: 1px; }
```

Learn more about customizing the spacing scale in the [theme variable documentation](/docs/theme).

### On this page

* [Quick reference](#quick-reference)
* [Examples](#examples)
  + [Basic example](#basic-example)
  + [Using a percentage](#using-a-percentage)
  + [Using the container scale](#using-the-container-scale)
  + [Using breakpoints container](#using-breakpoints-container)
  + [Using a custom value](#using-a-custom-value)
  + [Responsive design](#responsive-design)
* [Customizing your theme](#customizing-your-theme)
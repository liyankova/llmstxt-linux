---
source_url: "https://tailwindcss.com/docs/text-decoration-color"
title: "text-decoration-color - Typography - Tailwind CSS"
crawl_date: "2025-11-29T13:38:18.952693Z"
selector: ".isolate .mx-auto"
---

# text-decoration-color - Typography - Tailwind CSS

Typography

# text-decoration-color

Utilities for controlling the color of text decorations.

| Class | Styles |
| --- | --- |
| `decoration-inherit` | `text-decoration-color: inherit;` |
| `decoration-current` | `text-decoration-color: currentColor;` |
| `decoration-transparent` | `text-decoration-color: transparent;` |
| `decoration-black` | `text-decoration-color: var(--color-black); /* #000 */` |
| `decoration-white` | `text-decoration-color: var(--color-white); /* #fff */` |
| `decoration-red-50` | `text-decoration-color: var(--color-red-50); /* oklch(97.1% 0.013 17.38) */` |
| `decoration-red-100` | `text-decoration-color: var(--color-red-100); /* oklch(93.6% 0.032 17.717) */` |
| `decoration-red-200` | `text-decoration-color: var(--color-red-200); /* oklch(88.5% 0.062 18.334) */` |
| `decoration-red-300` | `text-decoration-color: var(--color-red-300); /* oklch(80.8% 0.114 19.571) */` |
| `decoration-red-400` | `text-decoration-color: var(--color-red-400); /* oklch(70.4% 0.191 22.216) */` |

Show more

## [Examples](#examples)

### [Basic example](#basic-example)

Use utilities like `decoration-sky-500` and `decoration-pink-500` to change the [text decoration](/docs/text-decoration-line) color of an element:

I’m Derek, an astro-engineer based in Tattooine. I like to build X-Wings at [My Company, Inc](#). Outside of work, I like to [watch pod-racing](#) and have [light-saber](#) fights.

```
<p>  I’m Derek, an astro-engineer based in Tattooine. I like to build X-Wings  at <a class="underline decoration-sky-500">My Company, Inc</a>. Outside  of work, I like to <a class="underline decoration-pink-500">watch pod-racing</a>  and have <a class="underline decoration-indigo-500">light-saber</a> fights.</p>
```

### [Changing the opacity](#changing-the-opacity)

Use the color opacity modifier to control the text decoration color opacity of an element:

I’m Derek, an astro-engineer based in Tattooine. I like to build X-Wings at [My Company, Inc](#). Outside of work, I like to [watch pod-racing](#) and have [light-saber](#) fights.

```
<p>  I’m Derek, an astro-engineer based in Tattooine. I like to build X-Wings  at <a class="underline decoration-sky-500/30">My Company, Inc</a>. Outside  of work, I like to <a class="underline decoration-pink-500/30">watch pod-racing</a>  and have <a class="underline decoration-indigo-500/30">light-saber</a> fights.</p>
```

### [Using a custom value](#using-a-custom-value)

Use the `decoration-[<value>]` syntax to set the text decoration color based on a completely custom value:

```
<p class="decoration-[#50d71e] ...">  Lorem ipsum dolor sit amet...</p>
```

For CSS variables, you can also use the `decoration-(<custom-property>)` syntax:

```
<p class="decoration-(--my-color) ...">  Lorem ipsum dolor sit amet...</p>
```

This is just a shorthand for `decoration-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Applying on hover](#applying-on-hover)

Prefix a `text-decoration-color` utility with a variant like `hover:*` to only apply the utility in that state:

Hover over the text to see the expected behavior

The [quick brown fox](https://en.wikipedia.org/wiki/The_quick_brown_fox_jumps_over_the_lazy_dog) jumps over the lazy dog.

```
<p>The <a href="..." class="underline hover:decoration-pink-500 ...">quick brown fox</a> jumps over the lazy dog.</p>
```

Learn more about using variants in the [variants documentation](/docs/hover-focus-and-other-states).

### [Responsive design](#responsive-design)

Prefix a `text-decoration-color` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<p class="underline decoration-sky-600 md:decoration-blue-400 ...">  Lorem ipsum dolor sit amet...</p>
```

Learn more about using variants in the [variants documentation](/docs/hover-focus-and-other-states).

## [Customizing your theme](#customizing-your-theme)

Use the `--color-*` theme variables to customize the color utilities in your project:

```
@theme {  --color-regal-blue: #243c5a; }
```

Now the `decoration-regal-blue` utility can be used in your markup:

```
<p class="decoration-regal-blue">  Lorem ipsum dolor sit amet...</p>
```

Learn more about customizing your theme in the [theme documentation](/docs/theme#customizing-your-theme).

### On this page

* [Quick reference](#quick-reference)
* [Examples](#examples)
  + [Basic example](#basic-example)
  + [Changing the opacity](#changing-the-opacity)
  + [Using a custom value](#using-a-custom-value)
  + [Applying on hover](#applying-on-hover)
  + [Responsive design](#responsive-design)
* [Customizing your theme](#customizing-your-theme)
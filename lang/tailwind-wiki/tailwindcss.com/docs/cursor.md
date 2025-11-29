---
source_url: "https://tailwindcss.com/docs/cursor"
title: "cursor - Interactivity - Tailwind CSS"
crawl_date: "2025-11-29T13:42:57.457971Z"
selector: ".isolate .mx-auto"
---

# cursor - Interactivity - Tailwind CSS

Interactivity

# cursor

Utilities for controlling the cursor style when hovering over an element.

| Class | Styles |
| --- | --- |
| `cursor-auto` | `cursor: auto;` |
| `cursor-default` | `cursor: default;` |
| `cursor-pointer` | `cursor: pointer;` |
| `cursor-wait` | `cursor: wait;` |
| `cursor-text` | `cursor: text;` |
| `cursor-move` | `cursor: move;` |
| `cursor-help` | `cursor: help;` |
| `cursor-not-allowed` | `cursor: not-allowed;` |
| `cursor-none` | `cursor: none;` |
| `cursor-context-menu` | `cursor: context-menu;` |

Show more

## [Examples](#examples)

### [Basic example](#basic-example)

Use utilities like `cursor-pointer` and `cursor-grab` to control which cursor is displayed when hovering over an element:

Hover over each button to see the cursor change

SubmitSaving...Confirm

```
<button class="cursor-pointer ...">Submit</button><button class="cursor-progress ...">Saving...</button><button class="cursor-not-allowed ..." disabled>Confirm</button>
```

### [Using a custom value](#using-a-custom-value)

Use the `cursor-[<value>]` syntax to set the cursor based on a completely custom value:

```
<button class="cursor-[url(hand.cur),_pointer] ...">  <!-- ... --></button>
```

For CSS variables, you can also use the `cursor-(<custom-property>)` syntax:

```
<button class="cursor-(--my-cursor) ...">  <!-- ... --></button>
```

This is just a shorthand for `cursor-[var(<custom-property>)]` that adds the `var()` function for you automatically.

### [Responsive design](#responsive-design)

Prefix a `cursor` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<button class="cursor-not-allowed md:cursor-auto ...">  <!-- ... --></button>
```

Learn more about using variants in the [variants documentation](/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](#quick-reference)
* [Examples](#examples)
  + [Basic example](#basic-example)
  + [Using a custom value](#using-a-custom-value)
  + [Responsive design](#responsive-design)
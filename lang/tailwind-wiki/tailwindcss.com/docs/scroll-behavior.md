---
source_url: "https://tailwindcss.com/docs/scroll-behavior"
title: "scroll-behavior - Interactivity - Tailwind CSS"
crawl_date: "2025-11-29T13:43:10.631101Z"
selector: ".isolate .mx-auto"
---

# scroll-behavior - Interactivity - Tailwind CSS

Interactivity

# scroll-behavior

Utilities for controlling the scroll behavior of an element.

| Class | Styles |
| --- | --- |
| `scroll-auto` | `scroll-behavior: auto;` |
| `scroll-smooth` | `scroll-behavior: smooth;` |

## [Examples](#examples)

### [Using smooth scrolling](#using-smooth-scrolling)

Use the `scroll-smooth` utility to enable smooth scrolling within an element:

```
<html class="scroll-smooth">  <!-- ... --></html>
```

Setting the `scroll-behavior` only affects scroll events that are triggered by the browser.

### [Using normal scrolling](#using-normal-scrolling)

Use the `scroll-auto` utility to revert to the default browser behavior for scrolling:

```
<html class="scroll-smooth md:scroll-auto">  <!-- ... --></html>
```

### On this page

* [Quick reference](#quick-reference)
* [Examples](#examples)
  + [Using smooth scrolling](#using-smooth-scrolling)
  + [Using normal scrolling](#using-normal-scrolling)
---
source_url: "https://tailwindcss.com/docs/flex-wrap"
title: "flex-wrap - Flexbox & Grid - Tailwind CSS"
crawl_date: "2025-11-29T13:33:37.525954Z"
selector: ".isolate .mx-auto"
---

# flex-wrap - Flexbox & Grid - Tailwind CSS

Flexbox & Grid

# flex-wrap

Utilities for controlling how flex items wrap.

| Class | Styles |
| --- | --- |
| `flex-nowrap` | `flex-wrap: nowrap;` |
| `flex-wrap` | `flex-wrap: wrap;` |
| `flex-wrap-reverse` | `flex-wrap: wrap-reverse;` |

## [Examples](#examples)

### [Don't wrap](#dont-wrap)

Use `flex-nowrap` to prevent flex items from wrapping, causing inflexible items to overflow the container if necessary:

01

02

03

```
<div class="flex flex-nowrap">  <div>01</div>  <div>02</div>  <div>03</div></div>
```

### [Wrap normally](#wrap-normally)

Use `flex-wrap` to allow flex items to wrap:

01

02

03

```
<div class="flex flex-wrap">  <div>01</div>  <div>02</div>  <div>03</div></div>
```

### [Wrap reversed](#wrap-reversed)

Use `flex-wrap-reverse` to wrap flex items in the reverse direction:

01

02

03

```
<div class="flex flex-wrap-reverse">  <div>01</div>  <div>02</div>  <div>03</div></div>
```

### [Responsive design](#responsive-design)

Prefix a `flex-wrap` utility with a breakpoint variant like `md:` to only apply the utility at medium screen sizes and above:

```
<div class="flex flex-wrap md:flex-wrap-reverse ...">  <!-- ... --></div>
```

Learn more about using variants in the [variants documentation](/docs/hover-focus-and-other-states).

### On this page

* [Quick reference](#quick-reference)
* [Examples](#examples)
  + [Don't wrap](#dont-wrap)
  + [Wrap normally](#wrap-normally)
  + [Wrap reversed](#wrap-reversed)
  + [Responsive design](#responsive-design)
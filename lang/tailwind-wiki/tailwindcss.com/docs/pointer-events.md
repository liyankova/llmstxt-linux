---
source_url: "https://tailwindcss.com/docs/pointer-events"
title: "pointer-events - Interactivity - Tailwind CSS"
crawl_date: "2025-11-29T13:43:02.722232Z"
selector: ".isolate .mx-auto"
---

# pointer-events - Interactivity - Tailwind CSS

Interactivity

# pointer-events

Utilities for controlling whether an element responds to pointer events.

| Class | Styles |
| --- | --- |
| `pointer-events-auto` | `pointer-events: auto;` |
| `pointer-events-none` | `pointer-events: none;` |

## [Examples](#examples)

### [Ignoring pointer events](#ignoring-pointer-events)

Use the `pointer-events-none` utility to make an element ignore pointer events, like `:hover` and `click` events:

Click the search icons to see the expected behavior

pointer-events-auto

pointer-events-none

```
<div class="relative ...">  <div class="pointer-events-auto absolute ...">    <svg class="absolute h-5 w-5 text-gray-400">      <!-- ... -->    </svg>  </div>  <input type="text" placeholder="Search" class="..." /></div><div class="relative ...">  <div class="pointer-events-none absolute ...">    <svg class="absolute h-5 w-5 text-gray-400">      <!-- ... -->    </svg>  </div>  <input type="text" placeholder="Search" class="..." /></div>
```

The pointer events will still trigger on child elements and pass-through to elements that are "beneath" the target.

### [Restoring pointer events](#restoring-pointer-events)

Use the `pointer-events-auto` utility to revert to the default browser behavior for pointer events:

```
<div class="pointer-events-none md:pointer-events-auto ...">  <!-- ... --></div>
```

### On this page

* [Quick reference](#quick-reference)
* [Examples](#examples)
  + [Ignoring pointer events](#ignoring-pointer-events)
  + [Restoring pointer events](#restoring-pointer-events)
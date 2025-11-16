---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/PopupAdjustment"
title: "Quickshell - PopupAdjustment"
crawl_date: "2025-11-16T14:37:18.160844Z"
selector: ".docslayout"
---

# Quickshell - PopupAdjustment

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [Flip](#Flip)
* [Resize](#Resize)
* [All](#All)
* [FlipX](#FlipX)
* [ResizeX](#ResizeX)
* [SlideY](#SlideY)
* [ResizeY](#ResizeY)
* [None](#None)
* [Slide](#Slide)
* [SlideX](#SlideX)
* [FlipY](#FlipY)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [PopupAdjustment](/docs/v0.2.1/types/Quickshell/PopupAdjustment)
 

---

## PopupAdjustment: PopupAdjustment

`import Quickshell`

Adjustment strategy for popups. See [PopupAnchor.adjustment](/docs/v0.2.1/types/Quickshell/PopupAnchor#adjustment).

Adjustment flags can be combined with the `|` operator.

`Flip` will be applied first, then `Slide`, then `Resize`.

 

## Variants

* Flip

  Alias for `FlipX | FlipY`.
* Resize

  Alias for `ResizeX | ResizeY`
* All

  Alias for `Flip | Slide | Resize`.
* FlipX

  If the X axis is constrained, the popup will invert its horizontal gravity if any.
* ResizeX

  If the X axis is constrained, the width of the popup will be reduced to fit on screen.
* SlideY

  If the Y axis is constrained, the popup will slide along the Y axis until it fits onscreen.
* ResizeY

  If the Y axis is constrained, the height of the popup will be reduced to fit on screen.
* None

  *No details provided*
* Slide

  Alias for `SlideX | SlideY`.
* SlideX

  If the X axis is constrained, the popup will slide along the X axis until it fits onscreen.
* FlipY

  If the Y axis is constrained, the popup will invert its vertical gravity if any.

* [Flip](#Flip)
* [Resize](#Resize)
* [All](#All)
* [FlipX](#FlipX)
* [ResizeX](#ResizeX)
* [SlideY](#SlideY)
* [ResizeY](#ResizeY)
* [None](#None)
* [Slide](#Slide)
* [SlideX](#SlideX)
* [FlipY](#FlipY)
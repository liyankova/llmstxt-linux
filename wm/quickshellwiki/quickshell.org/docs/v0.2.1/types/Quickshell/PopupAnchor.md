---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/PopupAnchor"
title: "Quickshell - PopupAnchor"
crawl_date: "2025-11-16T14:37:21.799575Z"
selector: ".docslayout"
---

# Quickshell - PopupAnchor

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [rect](#rect)
* [window](#window)
* [edges](#edges)
* [gravity](#gravity)
* [margins](#margins)
* [item](#item)
* [adjustment](#adjustment)

* [updateAnchor](#updateAnchor)

* [anchoring](#anchoring)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [PopupAnchor](/docs/v0.2.1/types/Quickshell/PopupAnchor)
 

---

## PopupAnchor: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell`

Anchorpoint or positioner for popup windows. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* rect  : 
  [[h,height,y,w,width,x]](#)

  h:[int](https://doc.qt.io/qt-6/qml-int.html)   height:[int](https://doc.qt.io/qt-6/qml-int.html)   y:[int](https://doc.qt.io/qt-6/qml-int.html)   w:[int](https://doc.qt.io/qt-6/qml-int.html)   width:[int](https://doc.qt.io/qt-6/qml-int.html)   x:[int](https://doc.qt.io/qt-6/qml-int.html)

  The anchorpoints the popup will attach to, relative to [item](#item) or [window](#window).
  Which anchors will be used is determined by the [edges](#edges), [gravity](#gravity), and [adjustment](#adjustment).

  If using [item](#item), the default anchor rectangle matches the dimensions of the item.

  If you leave [edges](#edges), [gravity](#gravity) and [adjustment](#adjustment) at their default values,
  setting more than `x` and `y` does not matter. The anchor rect cannot
  be smaller than 1x1 pixels.
* window  : 
  [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  The window to anchor / attach the popup to. Setting this property unsets [item](#item).
* edges  : 
  [Edges](/docs/v0.2.1/types/Quickshell/Edges)

  The point on the anchor rectangle the popup should anchor to.
  Opposing edges suchs as `Edges.Left | Edges.Right` are not allowed.

  Defaults to `Edges.Top | Edges.Left`.
* gravity  : 
  [Edges](/docs/v0.2.1/types/Quickshell/Edges)

  The direction the popup should expand towards, relative to the anchorpoint.
  Opposing edges suchs as `Edges.Left | Edges.Right` are not allowed.

  Defaults to `Edges.Bottom | Edges.Right`.
* margins  : 
  [[left,right,top,bottom]](#)

  left:[int](https://doc.qt.io/qt-6/qml-int.html)   right:[int](https://doc.qt.io/qt-6/qml-int.html)   top:[int](https://doc.qt.io/qt-6/qml-int.html)   bottom:[int](https://doc.qt.io/qt-6/qml-int.html)

  A margin applied to the anchor rect.

  This is most useful when [item](#item) is used and [rect](#rect) is left at its default
  value (matching the Item’s dimensions).
* item  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  The item to anchor / attach the popup to. Setting this property unsets [window](#window).

  The popup’s position relative to its parent window is only calculated when it is
  initially shown (directly before [anchoring()](#anchoring) is emitted), meaning its anchor
  rectangle will be set relative to the item’s position in the window at that time.
  [updateAnchor()](#updateAnchor) can be called to update the anchor rectangle if the item’s position
  has changed.

  NOTE

  If a more flexible way to position a popup relative to an item is needed,
  set [window](#window) to the item’s parent window, and handle the [anchoring](#anchoring) signal to
  position the popup relative to the window’s contentItem.
* adjustment  : 
  [PopupAdjustment](/docs/v0.2.1/types/Quickshell/PopupAdjustment)

  The strategy used to adjust the popup’s position if it would otherwise not fit on screen,
  based on the anchor [rect](#rect), preferred [edges](#edges), and [gravity](#gravity).

  See the documentation for [PopupAdjustment](/docs/v0.2.1/types/Quickshell/PopupAdjustment) for details.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* updateAnchor()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Update the popup’s anchor rect relative to its parent window.

  If anchored to an item, popups anchors will not automatically follow
  the item if its position changes. This function can be called to
  recalculate the anchors.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* anchoring()

  Emitted when this anchor is about to be used. Mostly useful for modifying
  the anchor [rect](#rect) using [coordinate mapping functions](https://doc.qt.io/qt-6/qml-qtquick-item.html#mapFromItem-method), which are not reactive.

* [rect](#rect)
* [window](#window)
* [edges](#edges)
* [gravity](#gravity)
* [margins](#margins)
* [item](#item)
* [adjustment](#adjustment)

* [updateAnchor](#updateAnchor)

* [anchoring](#anchoring)
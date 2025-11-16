---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Widgets/WrapperRectangle"
title: "Quickshell.Widgets - WrapperRectangle"
crawl_date: "2025-11-16T14:43:01.024675Z"
selector: ".docslayout"
---

# Quickshell.Widgets - WrapperRectangle

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [child](#child)
* [resizeChild](#resizeChild)
* [topMargin](#topMargin)
* [rightMargin](#rightMargin)
* [implicitHeight](#implicitHeight)
* [leftMargin](#leftMargin)
* [sets](#sets)
* [implicitWidth](#implicitWidth)
* [extraMargin](#extraMargin)
* [contentInsideBorder](#contentInsideBorder)
* [margin](#margin)
* [bottomMargin](#bottomMargin)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Widgets](/docs/v0.2.1/types/Quickshell.Widgets)
6. [WrapperRectangle](/docs/v0.2.1/types/Quickshell.Widgets/WrapperRectangle)
 

---

## WrapperRectangle: [Rectangle](https://doc.qt.io/qt-6/qml-qtquick-rectangle.html)

`import Quickshell.Widgets`

This component is useful for adding a border or background rectangle to
a child item. If you need to clip the child item to the rectangle’s
border, see [ClippingWrapperRectangle](/docs/v0.2.1/types/Quickshell.Widgets/ClippingWrapperRectangle).

NOTE

WrapperRectangle is a [MarginWrapperManager](/docs/v0.2.1/types/Quickshell.Widgets/MarginWrapperManager) based component.
See its documentation for information on how margins and sizes are calculated.

WARNING

You should not set [Item.x](/docs/v0.2.1/types/Quickshell.Widgets/Item#x), [Item.y](/docs/v0.2.1/types/Quickshell.Widgets/Item#y), [Item.width](/docs/v0.2.1/types/Quickshell.Widgets/Item#width),
[Item.height](/docs/v0.2.1/types/Quickshell.Widgets/Item#height) or [Item.anchors](/docs/v0.2.1/types/Quickshell.Widgets/Item#anchors) on the child item, as they are used
by WrapperItem to position it. Instead set [Item.implicitWidth](/docs/v0.2.1/types/Quickshell.Widgets/Item#implicitWidth) and
[Item.implicitHeight](/docs/v0.2.1/types/Quickshell.Widgets/Item#implicitHeight).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* child  : 
  [unknown](#unknown)

  See [WrapperManager.child](/docs/v0.2.1/types/Quickshell.Widgets/WrapperManager#child) for details.
* resizeChild  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Determines if child item should be resized larger than its implicit size if
  the parent is resized larger than its implicit size. Defaults to true.
* topMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested top margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.
* rightMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested right margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.
* implicitHeight  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Overrides the implicit height of the wrapper.

  Defaults to the implicit width of the content item plus its top and bottom margin,
  and may be reset by assigning `undefined`.
* leftMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested left margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.
* sets  : 
  [unknown](#unknown)

  *No details provided*
* implicitWidth  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Overrides the implicit width of the wrapper.

  Defaults to the implicit width of the content item plus its left and right margin,
  and may be reset by assigning `undefined`.
* extraMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  An extra margin applied in addition to [topMargin](#topMargin), [bottomMargin](#bottomMargin),
  [leftMargin](#leftMargin), and [rightMargin](#rightMargin).
  If [contentInsideBorder](#contentInsideBorder) is true, the rectangle’s border width will be added
  to this property. Defaults to 0.
* contentInsideBorder  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true (default), the rectangle’s border width will be added
  to [extraMargin](#extraMargin).
* margin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The default for [topMargin](#topMargin), [bottomMargin](#bottomMargin), [leftMargin](#leftMargin) and [rightMargin](#rightMargin).
  Defaults to 0.
* bottomMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested bottom margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.

* [child](#child)
* [resizeChild](#resizeChild)
* [topMargin](#topMargin)
* [rightMargin](#rightMargin)
* [implicitHeight](#implicitHeight)
* [leftMargin](#leftMargin)
* [sets](#sets)
* [implicitWidth](#implicitWidth)
* [extraMargin](#extraMargin)
* [contentInsideBorder](#contentInsideBorder)
* [margin](#margin)
* [bottomMargin](#bottomMargin)
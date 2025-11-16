---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Widgets/WrapperItem"
title: "Quickshell.Widgets - WrapperItem"
crawl_date: "2025-11-16T14:42:50.970619Z"
selector: ".docslayout"
---

# Quickshell.Widgets - WrapperItem

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [bottomMargin](#bottomMargin)
* [extraMargin](#extraMargin)
* [margin](#margin)
* [leftMargin](#leftMargin)
* [implicitHeight](#implicitHeight)
* [implicitWidth](#implicitWidth)
* [resizeChild](#resizeChild)
* [child](#child)
* [rightMargin](#rightMargin)
* [topMargin](#topMargin)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Widgets](/docs/v0.2.1/types/Quickshell.Widgets)
6. [WrapperItem](/docs/v0.2.1/types/Quickshell.Widgets/WrapperItem)
 

---

## WrapperItem: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

`import Quickshell.Widgets`

This component is useful when you need to wrap a single component in
an item, or give a single component a margin. See [QtQuick.Layouts](https://doc.qt.io/qt-6/qtquicklayouts-index.html)
for positioning multiple items.

NOTE

WrapperItem is a [MarginWrapperManager](/docs/v0.2.1/types/Quickshell.Widgets/MarginWrapperManager) based component.
See its documentation for information on how margins and sizes are calculated.

### Example: Adding a margin to an item

The snippet below adds a 10px margin to all sides of the [Text](https://doc.qt.io/qt-6/qml-qtquick-text.html) item.

```
WrapperItem {
  margin: 10

  Text { text: "Hello!" }
}
```

NOTE

The child item can be specified by writing it inline in the wrapper,
as in the example above, or by using the [child](#child) property. See
[WrapperManager.child](/docs/v0.2.1/types/Quickshell.Widgets/WrapperManager#child) for details.

WARNING

You should not set [Item.x](/docs/v0.2.1/types/Quickshell.Widgets/Item#x), [Item.y](/docs/v0.2.1/types/Quickshell.Widgets/Item#y), [Item.width](/docs/v0.2.1/types/Quickshell.Widgets/Item#width),
[Item.height](/docs/v0.2.1/types/Quickshell.Widgets/Item#height) or [Item.anchors](/docs/v0.2.1/types/Quickshell.Widgets/Item#anchors) on the child item, as they are used
by WrapperItem to position it. Instead set [Item.implicitWidth](/docs/v0.2.1/types/Quickshell.Widgets/Item#implicitWidth) and
[Item.implicitHeight](/docs/v0.2.1/types/Quickshell.Widgets/Item#implicitHeight).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* bottomMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested bottom margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.
* extraMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  An extra margin applied in addition to [topMargin](#topMargin), [bottomMargin](#bottomMargin),
  [leftMargin](#leftMargin), and [rightMargin](#rightMargin). Defaults to 0.
* margin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The default for [topMargin](#topMargin), [bottomMargin](#bottomMargin), [leftMargin](#leftMargin) and [rightMargin](#rightMargin).
  Defaults to 0.
* leftMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested left margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.
* implicitHeight  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Overrides the implicit height of the wrapper.

  Defaults to the implicit width of the content item plus its top and bottom margin,
  and may be reset by assigning `undefined`.
* implicitWidth  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Overrides the implicit width of the wrapper.

  Defaults to the implicit width of the content item plus its left and right margin,
  and may be reset by assigning `undefined`.
* resizeChild  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Determines if child item should be resized larger than its implicit size if
  the parent is resized larger than its implicit size. Defaults to true.
* child  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  See [WrapperManager.child](/docs/v0.2.1/types/Quickshell.Widgets/WrapperManager#child) for details.
* rightMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested right margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.
* topMargin  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The requested top margin of the content item, not counting [extraMargin](#extraMargin).

  Defaults to [margin](#margin), and may be reset by assigning `undefined`.

* [bottomMargin](#bottomMargin)
* [extraMargin](#extraMargin)
* [margin](#margin)
* [leftMargin](#leftMargin)
* [implicitHeight](#implicitHeight)
* [implicitWidth](#implicitWidth)
* [resizeChild](#resizeChild)
* [child](#child)
* [rightMargin](#rightMargin)
* [topMargin](#topMargin)
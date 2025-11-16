---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Widgets/ClippingRectangle"
title: "Quickshell.Widgets - ClippingRectangle"
crawl_date: "2025-11-16T14:42:36.909944Z"
selector: ".docslayout"
---

# Quickshell.Widgets - ClippingRectangle

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [color](#color)
* [contentItem](#contentItem)
* [contentUnderBorder](#contentUnderBorder)
* [topLeftRadius](#topLeftRadius)
* [border](#border)
* [radius](#radius)
* [topRightRadius](#topRightRadius)
* [data](#data)
* [antialiasing](#antialiasing)
* [bottomLeftRadius](#bottomLeftRadius)
* [bottomRightRadius](#bottomRightRadius)
* [children](#children)
* [contentInsideBorder](#contentInsideBorder)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Widgets](/docs/v0.2.1/types/Quickshell.Widgets)
6. [ClippingRectangle](/docs/v0.2.1/types/Quickshell.Widgets/ClippingRectangle)
 

---

## ClippingRectangle: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

`import Quickshell.Widgets`

WARNING

This type requires at least Qt 6.7.

This is a specialized version of [Rectangle](https://doc.qt.io/qt-6/qml-qtquick-rectangle.html) that clips content
inside of its border, including rounded rectangles. It costs more than
[Rectangle](https://doc.qt.io/qt-6/qml-qtquick-rectangle.html), so it should not be used unless you need to clip
items inside of it to the border.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* color  : 
  [color](https://doc.qt.io/qt-6/qml-color.html)

  The background color of the rectangle, which goes under its content.
* contentItem  : 
  [unknown](#unknown)

  readonly

  The item containing the rectangle’s content.
  There is usually no reason to use this directly.
* contentUnderBorder  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If content should be displayed underneath the border.

  Defaults to false, does nothing if the border is opaque.
* topLeftRadius  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Radius of the top left corner. Defaults to [radius](#radius).
* border  : 
  [unknown](#unknown)

  See [Rectangle.border](https://doc.qt.io/qt-6/qml-qtquick-rectangle.html#border-prop).
* radius  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Radius of all corners. Defaults to 0.
* topRightRadius  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Radius of the top right corner. Defaults to [radius](#radius).
* data  : 
  [unknown](#unknown)

  default

  Data of the ClippingRectangle’s [contentItem](#contentItem). (`list<QtObject>`).

  See [Item.data](https://doc.qt.io/qt-6/qml-qtquick-item.html#data-prop) for details.
* antialiasing  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the rectangle should be antialiased.

  Defaults to true if any corner has a non-zero radius, otherwise false.
* bottomLeftRadius  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Radius of the bottom left corner. Defaults to [radius](#radius).
* bottomRightRadius  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Radius of the bottom right corner. Defaults to [radius](#radius).
* children  : 
  [unknown](#unknown)

  Visual children of the ClippingRectangle’s [contentItem](#contentItem). (`list<Item>`).

  See [Item.children](https://doc.qt.io/qt-6/qml-qtquick-item.html#children-prop) for details.
* contentInsideBorder  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the content item should be resized to fit inside the border.

  Defaults to `!contentUnderBorder`. Most useful when combined with
  `anchors.fill: parent` on an item passed to the ClippingRectangle.

* [color](#color)
* [contentItem](#contentItem)
* [contentUnderBorder](#contentUnderBorder)
* [topLeftRadius](#topLeftRadius)
* [border](#border)
* [radius](#radius)
* [topRightRadius](#topRightRadius)
* [data](#data)
* [antialiasing](#antialiasing)
* [bottomLeftRadius](#bottomLeftRadius)
* [bottomRightRadius](#bottomRightRadius)
* [children](#children)
* [contentInsideBorder](#contentInsideBorder)
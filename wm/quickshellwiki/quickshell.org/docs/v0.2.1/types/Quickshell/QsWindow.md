---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/QsWindow"
title: "Quickshell - QsWindow"
crawl_date: "2025-11-16T14:37:45.843629Z"
selector: ".docslayout"
---

# Quickshell - QsWindow

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [data](#data)
* [devicePixelRatio](#devicePixelRatio)
* [width](#width)
* [visible](#visible)
* [implicitHeight](#implicitHeight)
* [contentItem](#contentItem)
* [height](#height)
* [surfaceFormat](#surfaceFormat)
* [color](#color)
* [backingWindowVisible](#backingWindowVisible)
* [implicitWidth](#implicitWidth)
* [mask](#mask)
* [screen](#screen)
* [windowTransform](#windowTransform)

* [itemPosition](#itemPosition)
* [itemRect](#itemRect)
* [mapFromItem](#mapFromItem)
* [mapFromItem](#mapFromItem)
* [mapFromItem](#mapFromItem)
* [mapFromItem](#mapFromItem)

* [resourcesLost](#resourcesLost)
* [closed](#closed)
* [windowConnected](#windowConnected)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [QsWindow](/docs/v0.2.1/types/Quickshell/QsWindow)
 

---

## QsWindow: [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)

uncreatable

`import Quickshell`

Base class of Quickshell windows

### Attached properties

`QSWindow` can be used as an attached object of anything that subclasses [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html).
It provides the following properties

* `window` - the `QSWindow` object.
* `contentItem` - the `contentItem` property of the window.

[itemPosition()](#itemPosition), [itemRect()](#itemRect), and [mapFromItem()](#mapFromItem) can also be called directly
on the attached object.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* data  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)>

  default  readonly

  *No details provided*
* devicePixelRatio  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  The ratio between logical pixels and monitor pixels.

  Qt’s coordinate system works in logical pixels, which equal N monitor pixels
  depending on scale factor. This property returns the amount of monitor pixels
  in a logical pixel for the current window.
* width  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  The window’s actual width.

  Setting this property is deprecated. Set [implicitWidth](#implicitWidth) instead.
* visible  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the window should be shown or hidden. Defaults to true.
* implicitHeight  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  The window’s desired height.
* contentItem  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  readonly

  *No details provided*
* height  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  The window’s actual height.

  Setting this property is deprecated. Set [implicitHeight](#implicitHeight) instead.
* surfaceFormat  : 
  [[opaque]](#)

  opaque:[bool](https://doc.qt.io/qt-6/qml-bool.html)

  Set the surface format to request from the system.

  + `opaque` - If the requested surface should be opaque. Opaque windows allow
    the operating system to avoid drawing things behind them, or blending the window
    with those behind it, saving power and GPU load. If unset, this property defaults to
    true if [color](#color) is opaque, or false if not. *You should not need to modify this
    property unless you create a surface that starts opaque and later becomes transparent.*

  NOTE

  The surface format cannot be changed after the window is created.
* color  : 
  [color](https://doc.qt.io/qt-6/qml-color.html)

  The background color of the window. Defaults to white.

  WARNING

  If the window color is opaque before it is made visible,
  it will not be able to become transparent later unless [surfaceFormat](#surfaceFormat).opaque
  is false.
* backingWindowVisible  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the window is currently shown. You should generally prefer [visible](#prop.visible).

  This property is useful for ensuring windows spawn in a specific order, and you should
  not use it in place of [visible](#prop.visible).
* implicitWidth  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  The window’s desired width.
* mask  : 
  [Region](/docs/v0.2.1/types/Quickshell/Region)

  The clickthrough mask. Defaults to null.

  If non null then the clickable areas of the window will be determined by the provided region.

  ```
  ShellWindow {
    // The mask region is set to `rect`, meaning only `rect` is clickable.
    // All other clicks pass through the window to ones behind it.
    mask: Region { item: rect }

    Rectangle {
      id: rect

      anchors.centerIn: parent
      width: 100
      height: 100
    }
  }
  ```

  If the provided region’s intersection mode is `Combine` (the default),
  then the region will be used as is. Otherwise it will be applied on top of the window region.

  For example, setting the intersection mode to `Xor` will invert the mask and make everything in
  the mask region not clickable and pass through clicks inside it through the window.

  ```
  ShellWindow {
    // The mask region is set to `rect`, but the intersection mode is set to `Xor`.
    // This inverts the mask causing all clicks inside `rect` to be passed to the window
    // behind this one.
    mask: Region { item: rect; intersection: Intersection.Xor }

    Rectangle {
      id: rect

      anchors.centerIn: parent
      width: 100
      height: 100
    }
  }
  ```
* screen  : 
  [ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)

  The screen that the window currently occupies.

  This may be modified to move the window to the given screen.
* windowTransform  : 
  [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  readonly

  Opaque property that will receive an update when factors that affect the window’s position
  and transform changed.

  This property is intended to be used to force a binding update,
  along with map[To|From]Item (which is not reactive).

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* itemPosition(item)  : 
  [point](https://doc.qt.io/qt-6/qml-point.html)

  item: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  Returns the given Item’s position relative to the window. Does not update reactively.

  Equivalent to calling `window.contentItem.mapFromItem(item, 0, 0)`

  See also: [Item.mapFromItem()](https://doc.qt.io/qt-6/qml-qtquick-item.html#mapFromItem-method)
* itemRect(item)  : 
  [rect](https://doc.qt.io/qt-6/qml-rect.html)

  item: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  Returns the given Item’s geometry relative to the window. Does not update reactively.

  Equivalent to calling `window.contentItem.mapFromItem(item, 0, 0, 0, 0)`

  See also: [Item.mapFromItem()](https://doc.qt.io/qt-6/qml-qtquick-item.html#mapFromItem-method)
* mapFromItem(item, point)  : 
  [point](https://doc.qt.io/qt-6/qml-point.html)

  item: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)   point: [point](https://doc.qt.io/qt-6/qml-point.html)

  Maps the given point in the coordinate space of `item` to one in the coordinate space
  of this window. Does not update reactively.

  Equivalent to calling `window.contentItem.mapFromItem(item, point)`

  See also: [Item.mapFromItem()](https://doc.qt.io/qt-6/qml-qtquick-item.html#mapFromItem-method)
* mapFromItem(item, x, y)  : 
  [point](https://doc.qt.io/qt-6/qml-point.html)

  item: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)   x: [real](https://doc.qt.io/qt-6/qml-real.html)   y: [real](https://doc.qt.io/qt-6/qml-real.html)

  Maps the given point in the coordinate space of `item` to one in the coordinate space
  of this window. Does not update reactively.

  Equivalent to calling `window.contentItem.mapFromItem(item, x, y)`

  See also: [Item.mapFromItem()](https://doc.qt.io/qt-6/qml-qtquick-item.html#mapFromItem-method)
* mapFromItem(item, rect)  : 
  [rect](https://doc.qt.io/qt-6/qml-rect.html)

  item: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)   rect: [rect](https://doc.qt.io/qt-6/qml-rect.html)

  Maps the given rect in the coordinate space of `item` to one in the coordinate space
  of this window. Does not update reactively.

  Equivalent to calling `window.contentItem.mapFromItem(item, rect)`

  See also: [Item.mapFromItem()](https://doc.qt.io/qt-6/qml-qtquick-item.html#mapFromItem-method)
* mapFromItem(item, x, y, width, height)  : 
  [rect](https://doc.qt.io/qt-6/qml-rect.html)

  item: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)   x: [real](https://doc.qt.io/qt-6/qml-real.html)   y: [real](https://doc.qt.io/qt-6/qml-real.html)   width: [real](https://doc.qt.io/qt-6/qml-real.html)   height: [real](https://doc.qt.io/qt-6/qml-real.html)

  Maps the given rect in the coordinate space of `item` to one in the coordinate space
  of this window. Does not update reactively.

  Equivalent to calling `window.contentItem.mapFromItem(item, x, y, width, height)`

  See also: [Item.mapFromItem()](https://doc.qt.io/qt-6/qml-qtquick-item.html#mapFromItem-method)

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* resourcesLost()

  This signal is emitted when resources a window depends on to display are lost,
  or could not be acquired during window creation. The most common trigger for
  this signal is a lack of VRAM when creating or resizing a window.

  Following this signal, [closed()](#closed) will be sent.
* closed()

  This signal is emitted when the window is closed by the user, the display server,
  or an error. It is not emitted when [visible](#visible) is set to false.
* windowConnected()

  *No details provided*

* [data](#data)
* [devicePixelRatio](#devicePixelRatio)
* [width](#width)
* [visible](#visible)
* [implicitHeight](#implicitHeight)
* [contentItem](#contentItem)
* [height](#height)
* [surfaceFormat](#surfaceFormat)
* [color](#color)
* [backingWindowVisible](#backingWindowVisible)
* [implicitWidth](#implicitWidth)
* [mask](#mask)
* [screen](#screen)
* [windowTransform](#windowTransform)

* [itemPosition](#itemPosition)
* [itemRect](#itemRect)
* [mapFromItem](#mapFromItem)
* [mapFromItem](#mapFromItem)
* [mapFromItem](#mapFromItem)
* [mapFromItem](#mapFromItem)

* [resourcesLost](#resourcesLost)
* [closed](#closed)
* [windowConnected](#windowConnected)
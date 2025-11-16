---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Widgets/IconImage"
title: "Quickshell.Widgets - IconImage"
crawl_date: "2025-11-16T14:42:43.906577Z"
selector: ".docslayout"
---

# Quickshell.Widgets - IconImage

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [source](#source)
* [asynchronous](#asynchronous)
* [backer](#backer)
* [implicitSize](#implicitSize)
* [mipmap](#mipmap)
* [actualSize](#actualSize)
* [status](#status)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Widgets](/docs/v0.2.1/types/Quickshell.Widgets)
6. [IconImage](/docs/v0.2.1/types/Quickshell.Widgets/IconImage)
 

---

## IconImage: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

`import Quickshell.Widgets`

This is a specialization of [Image](https://doc.qt.io/qt-6/qml-qtquick-image.html) configured for icon-style images,
designed to make it easier to use correctly. If you need more control, use
[Image](https://doc.qt.io/qt-6/qml-qtquick-image.html) directly.

The image’s aspect raito is assumed to be 1:1. If it is not 1:1, padding
will be added to make it 1:1. This is currently applied before the actual
aspect ratio of the image is taken into account, and may change in a future
release.

You should use it for:

* Icons for custom buttons
* Status indicator icons
* System tray icons
* Things similar to the above.

Do not use it for:

* Big images
* Images that change size frequently
* Anything that doesn’t feel like an icon.

NOTE

More information about many of these properties can be found in
the documentation for [Image](https://doc.qt.io/qt-6/qml-qtquick-image.html).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* source  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  URL of the image. Defaults to an empty string.
  See [Image.source](https://doc.qt.io/qt-6/qml-qtquick-image.html#source-prop).
* asynchronous  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the image should be loaded asynchronously. Defaults to false.
  See [Image.asynchronous](https://doc.qt.io/qt-6/qml-qtquick-image.html#asynchronous-prop).
* backer  : 
  [Image](https://doc.qt.io/qt-6/qml-qtquick-image.html)

  The [Image](https://doc.qt.io/qt-6/qml-qtquick-image.html) backing this object.

  This is useful if you need to access more functionality than
  exposed by IconImage.
* implicitSize  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The suggested size of the image. This is used as a defualt
  for [Item.implicitWidth](https://doc.qt.io/qt-6/qml-qtquick-item.html#implicitWidth-prop) and [Item.implicitHeight](https://doc.qt.io/qt-6/qml-qtquick-item.html#implicitHeight-prop).
* mipmap  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the image should be mipmap filtered. Defaults to false.
  See [Image.mipmap](https://doc.qt.io/qt-6/qml-qtquick-image.html#mipmap-prop).

  Try enabling this if your image is significantly scaled down
  and looks bad because of it.
* actualSize  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  The actual size the image will be displayed at.
* status  : 
  [unknown](#unknown)

  The load status of the image. See [Image.status](https://doc.qt.io/qt-6/qml-qtquick-image.html#status-prop).

* [source](#source)
* [asynchronous](#asynchronous)
* [backer](#backer)
* [implicitSize](#implicitSize)
* [mipmap](#mipmap)
* [actualSize](#actualSize)
* [status](#status)
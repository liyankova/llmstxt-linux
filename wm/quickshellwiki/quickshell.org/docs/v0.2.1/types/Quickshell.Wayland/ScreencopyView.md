---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Wayland/ScreencopyView"
title: "Quickshell.Wayland - ScreencopyView"
crawl_date: "2025-11-16T14:42:13.410067Z"
selector: ".docslayout"
---

# Quickshell.Wayland - ScreencopyView

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [live](#live)
* [paintCursor](#paintCursor)
* [constraintSize](#constraintSize)
* [sourceSize](#sourceSize)
* [captureSource](#captureSource)
* [hasContent](#hasContent)

* [captureFrame](#captureFrame)

* [stopped](#stopped)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Wayland](/docs/v0.2.1/types/Quickshell.Wayland)
6. [ScreencopyView](/docs/v0.2.1/types/Quickshell.Wayland/ScreencopyView)
 

---

## ScreencopyView: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

`import Quickshell.Wayland`

ScreencopyView displays live video streams or single captured frames from valid
capture sources. See [captureSource](#captureSource) for details on which objects are accepted.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* live  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true, a live video feed from the capture source will be displayed instead of a still image.
  Defaults to false.
* paintCursor  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true, the system cursor will be painted on the image. Defaults to false.
* constraintSize  : 
  [unknown](#unknown)

  If nonzero, the width and height constraints set for this property will constrain those
  dimensions of the ScreencopyView’s implicit size, maintaining the image’s aspect ratio.
* sourceSize  : 
  [size](https://doc.qt.io/qt-6/qml-size.html)

  readonly

  The size of the source image. Valid when [hasContent](#hasContent) is true.
* captureSource  : 
  [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  The object to capture from. Accepts any of the following:

  + `null` - Clears the displayed image.
  + [ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen) - A monitor.
    Requires a compositor that supports `wlr-screencopy-unstable`
    or both `ext-image-copy-capture-v1` and `ext-capture-source-v1`.
  + [Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel) - A toplevel window.
    Requires a compositor that supports `hyprland-toplevel-export-v1`.
* hasContent  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If true, the view has content ready to display. Content is not always immediately available,
  and this property can be used to avoid displaying it until ready.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* captureFrame()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Capture a single frame. Has no effect if [live](#live) is true.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* stopped()

  The compositor has ended the video stream. Attempting to restart it may or may not work.

* [live](#live)
* [paintCursor](#paintCursor)
* [constraintSize](#constraintSize)
* [sourceSize](#sourceSize)
* [captureSource](#captureSource)
* [hasContent](#hasContent)

* [captureFrame](#captureFrame)

* [stopped](#stopped)
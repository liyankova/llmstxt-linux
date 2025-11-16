---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.I3/I3Monitor"
title: "Quickshell.I3 - I3Monitor"
crawl_date: "2025-11-16T14:39:28.614013Z"
selector: ".docslayout"
---

# Quickshell.I3 - I3Monitor

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [focusedWorkspace](#focusedWorkspace)
* [id](#id)
* [scale](#scale)
* [height](#height)
* [width](#width)
* [lastIpcObject](#lastIpcObject)
* [name](#name)
* [power](#power)
* [x](#x)
* [y](#y)
* [activeWorkspace](#activeWorkspace)
* [focused](#focused)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.I3](/docs/v0.2.1/types/Quickshell.I3)
6. [I3Monitor](/docs/v0.2.1/types/Quickshell.I3/I3Monitor)
 

---

## I3Monitor: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.I3`

I3/Sway monitors 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* focusedWorkspace  : 
  [I3Workspace](/docs/v0.2.1/types/Quickshell.I3/I3Workspace)

  readonly

  Deprecated: See [activeWorkspace](#activeWorkspace).
* id  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The ID of this monitor
* scale  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  The scaling factor of this monitor, 1 means it runs at native resolution
* height  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The height in pixels of this monitor
* width  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The width in pixels of this monitor
* lastIpcObject  : 
  [unknown](#unknown)

  readonly

  Last JSON returned for this monitor, as a JavaScript object.

  This updates every time Quickshell receives an `output` event from i3/Sway
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The name of this monitor
* power  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  Wether this monitor is turned on or not
* x  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The X coordinate of this monitor inside the monitor layout
* y  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The Y coordinate of this monitor inside the monitor layout
* activeWorkspace  : 
  [I3Workspace](/docs/v0.2.1/types/Quickshell.I3/I3Workspace)

  readonly

  The currently active workspace on this monitor, May be null.
* focused  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  Whether this monitor is currently in focus

* [focusedWorkspace](#focusedWorkspace)
* [id](#id)
* [scale](#scale)
* [height](#height)
* [width](#width)
* [lastIpcObject](#lastIpcObject)
* [name](#name)
* [power](#power)
* [x](#x)
* [y](#y)
* [activeWorkspace](#activeWorkspace)
* [focused](#focused)
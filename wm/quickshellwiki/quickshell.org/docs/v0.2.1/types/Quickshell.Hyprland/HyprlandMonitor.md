---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandMonitor"
title: "Quickshell.Hyprland - HyprlandMonitor"
crawl_date: "2025-11-16T14:39:06.578220Z"
selector: ".docslayout"
---

# Quickshell.Hyprland - HyprlandMonitor

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [scale](#scale)
* [height](#height)
* [id](#id)
* [focused](#focused)
* [x](#x)
* [width](#width)
* [y](#y)
* [description](#description)
* [lastIpcObject](#lastIpcObject)
* [name](#name)
* [activeWorkspace](#activeWorkspace)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Hyprland](/docs/v0.2.1/types/Quickshell.Hyprland)
6. [HyprlandMonitor](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandMonitor)
 

---

## HyprlandMonitor: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Hyprland`

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* scale  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  *No details provided*
* height  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* id  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* focused  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the monitor is currently focused.
* x  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* width  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* y  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* description  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* lastIpcObject  : 
  [unknown](#unknown)

  readonly

  Last json returned for this monitor, as a javascript object.

  WARNING

  This is *not* updated unless the monitor object is fetched again from
  Hyprland. If you need a value that is subject to change and does not have a dedicated
  property, run [Hyprland.refreshMonitors()](/docs/v0.2.1/types/Quickshell.Hyprland/Hyprland#refreshMonitors) and wait for this property to update.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* activeWorkspace  : 
  [HyprlandWorkspace](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandWorkspace)

  readonly

  The currently active workspace on this monitor. May be null.

* [scale](#scale)
* [height](#height)
* [id](#id)
* [focused](#focused)
* [x](#x)
* [width](#width)
* [y](#y)
* [description](#description)
* [lastIpcObject](#lastIpcObject)
* [name](#name)
* [activeWorkspace](#activeWorkspace)
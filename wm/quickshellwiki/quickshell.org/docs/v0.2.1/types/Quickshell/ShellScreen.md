---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/ShellScreen"
title: "Quickshell - ShellScreen"
crawl_date: "2025-11-16T14:38:18.194439Z"
selector: ".docslayout"
---

# Quickshell - ShellScreen

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [physicalPixelDensity](#physicalPixelDensity)
* [height](#height)
* [primaryOrientation](#primaryOrientation)
* [serialNumber](#serialNumber)
* [name](#name)
* [x](#x)
* [logicalPixelDensity](#logicalPixelDensity)
* [devicePixelRatio](#devicePixelRatio)
* [y](#y)
* [width](#width)
* [model](#model)
* [orientation](#orientation)

* [toString](#toString)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)
 

---

## ShellScreen: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell`

Monitor object useful for setting the monitor for a [QsWindow](/docs/v0.2.1/types/Quickshell/QsWindow)
or querying information about the monitor.

WARNING

If the monitor is disconnected than any stored copies of its ShellMonitor will
be marked as dangling and all properties will return default values.
Reconnecting the monitor will not reconnect it to the ShellMonitor object.

Due to some technical limitations, it was not possible to reuse the native qml [Screen](https://doc.qt.io/qt-6/qml-qtquick-screen.html) type.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* physicalPixelDensity  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  The number of physical pixels per millimeter.
* height  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* primaryOrientation  : 
  [unknown](#unknown)

  readonly

  *No details provided*
* serialNumber  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The serial number of the screen as seen by the operating system.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The name of the screen as seen by the operating system.

  Usually something like `DP-1`, `HDMI-1`, `eDP-1`.
* x  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* logicalPixelDensity  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  The number of device-independent (scaled) pixels per millimeter.
* devicePixelRatio  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  The ratio between physical pixels and device-independent (scaled) pixels.
* y  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* width  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* model  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The model of the screen as seen by the operating system.
* orientation  : 
  [unknown](#unknown)

  readonly

  *No details provided*

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* toString()  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  *No details provided*

* [physicalPixelDensity](#physicalPixelDensity)
* [height](#height)
* [primaryOrientation](#primaryOrientation)
* [serialNumber](#serialNumber)
* [name](#name)
* [x](#x)
* [logicalPixelDensity](#logicalPixelDensity)
* [devicePixelRatio](#devicePixelRatio)
* [y](#y)
* [width](#width)
* [model](#model)
* [orientation](#orientation)

* [toString](#toString)
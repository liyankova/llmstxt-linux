---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLockSurface"
title: "Quickshell.Wayland - WlSessionLockSurface"
crawl_date: "2025-11-16T14:42:25.150020Z"
selector: ".docslayout"
---

# Quickshell.Wayland - WlSessionLockSurface

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [height](#height)
* [contentItem](#contentItem)
* [screen](#screen)
* [visible](#visible)
* [width](#width)
* [data](#data)
* [color](#color)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Wayland](/docs/v0.2.1/types/Quickshell.Wayland)
6. [WlSessionLockSurface](/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLockSurface)
 

---

## WlSessionLockSurface: [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)

`import Quickshell.Wayland`

Surface displayed by a [WlSessionLock](/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLock) when it is locked.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* height  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* contentItem  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  readonly

  *No details provided*
* screen  : 
  [ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)

  readonly

  The screen that the surface is displayed on.
* visible  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the surface has been made visible.

  Note: SessionLockSurfaces will never become invisible, they will only be destroyed.
* width  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* data  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)>

  default  readonly

  *No details provided*
* color  : 
  [color](https://doc.qt.io/qt-6/qml-color.html)

  The background color of the window. Defaults to white.

  WARNING

  This seems to behave weirdly when using transparent colors on some systems.
  Using a colored content item over a transparent window is the recommended way to work around this:

  ```
  ProxyWindow {
    Rectangle {
      anchors.fill: parent
      color: "#20ffffff"

      // your content here
    }
  }
  ```

  … but you probably shouldn’t make a transparent lock,
  and most compositors will ignore an attempt to do so.

* [height](#height)
* [contentItem](#contentItem)
* [screen](#screen)
* [visible](#visible)
* [width](#width)
* [data](#data)
* [color](#color)
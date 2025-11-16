---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Wayland/Toplevel"
title: "Quickshell.Wayland - Toplevel"
crawl_date: "2025-11-16T14:42:16.563245Z"
selector: ".docslayout"
---

# Quickshell.Wayland - Toplevel

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [minimized](#minimized)
* [parent](#parent)
* [title](#title)
* [maximized](#maximized)
* [screens](#screens)
* [appId](#appId)
* [activated](#activated)
* [fullscreen](#fullscreen)

* [activate](#activate)
* [close](#close)
* [fullscreenOn](#fullscreenOn)
* [setRectangle](#setRectangle)
* [unsetRectangle](#unsetRectangle)

* [closed](#closed)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Wayland](/docs/v0.2.1/types/Quickshell.Wayland)
6. [Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel)
 

---

## Toplevel: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Wayland`

A window/toplevel from another application, retrievable from
the [ToplevelManager](/docs/v0.2.1/types/Quickshell.Wayland/ToplevelManager).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* minimized  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the window is currently minimized.

  Minimization can be requested by setting this property, though it may
  be ignored by the compositor.
* parent  : 
  [Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel)

  readonly

  Parent toplevel if this toplevel is a modal/dialog, otherwise null.
* title  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* maximized  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the window is currently maximized.

  Maximization can be requested by setting this property, though it may
  be ignored by the compositor.
* screens  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)>

  readonly

  Screens the toplevel is currently visible on.
  Screens are listed in the order they have been added by the compositor.

  NOTE

  Some compositors only list a single screen, even if a window is visible on multiple.
* appId  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* activated  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the window is currently activated or focused.

  Activation can be requested with the [activate()](#activate) function.
* fullscreen  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the window is currently fullscreen.

  Fullscreen can be requested by setting this property, though it may
  be ignored by the compositor.
  Fullscreen can be requested on a specific screen with the [fullscreenOn()](#fullscreenOn) function.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* activate()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Request that this toplevel is activated.
  The request may be ignored by the compositor.
* close()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Request that this toplevel is closed.
  The request may be ignored by the compositor or the application.
* fullscreenOn(screen)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  screen: [ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)

  Request that this toplevel is fullscreened on a specific screen.
  The request may be ignored by the compositor.
* setRectangle(window, rect)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  window: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)   rect: [rect](https://doc.qt.io/qt-6/qml-rect.html)

  Provide a hint to the compositor where the visual representation
  of this toplevel is relative to a quickshell window.
  This hint can be used visually in operations like minimization.
* unsetRectangle()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  *No details provided*

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* closed()

  *No details provided*

* [minimized](#minimized)
* [parent](#parent)
* [title](#title)
* [maximized](#maximized)
* [screens](#screens)
* [appId](#appId)
* [activated](#activated)
* [fullscreen](#fullscreen)

* [activate](#activate)
* [close](#close)
* [fullscreenOn](#fullscreenOn)
* [setRectangle](#setRectangle)
* [unsetRectangle](#unsetRectangle)

* [closed](#closed)
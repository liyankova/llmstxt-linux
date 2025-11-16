---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.SystemTray/SystemTrayItem"
title: "Quickshell.Services.SystemTray - SystemTrayItem"
crawl_date: "2025-11-16T14:41:49.311127Z"
selector: ".docslayout"
---

# Quickshell.Services.SystemTray - SystemTrayItem

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [menu](#menu)
* [status](#status)
* [tooltipDescription](#tooltipDescription)
* [icon](#icon)
* [onlyMenu](#onlyMenu)
* [category](#category)
* [title](#title)
* [tooltipTitle](#tooltipTitle)
* [hasMenu](#hasMenu)
* [id](#id)

* [activate](#activate)
* [display](#display)
* [scroll](#scroll)
* [secondaryActivate](#secondaryActivate)

* [ready](#ready)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.SystemTray](/docs/v0.2.1/types/Quickshell.Services.SystemTray)
6. [SystemTrayItem](/docs/v0.2.1/types/Quickshell.Services.SystemTray/SystemTrayItem)
 

---

## SystemTrayItem: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.SystemTray`

A system tray item, roughly conforming to the [kde/freedesktop spec](https://www.freedesktop.org/wiki/Specifications/StatusNotifierItem/StatusNotifierItem/)
(there is no real spec, we just implemented whatever seemed to actually be used).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* menu  : 
  [unknown](#unknown)

  readonly

  A handle to the menu associated with this tray item, if any.

  Can be displayed with [QsMenuAnchor](/docs/v0.2.1/types/Quickshell/QsMenuAnchor) or [QsMenuOpener](/docs/v0.2.1/types/Quickshell/QsMenuOpener).
* status  : 
  [Status](/docs/v0.2.1/types/Quickshell.Services.SystemTray/Status)

  readonly

  *No details provided*
* tooltipDescription  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* icon  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Icon source string, usable as an Image source.
* onlyMenu  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this tray item only offers a menu and activation will do nothing.
* category  : 
  [Category](/docs/v0.2.1/types/Quickshell.Services.SystemTray/Category)

  readonly

  *No details provided*
* title  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Text that describes the application.
* tooltipTitle  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* hasMenu  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this tray item has an associated menu accessible via [display()](#display) or [menu](#menu).
* id  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  A name unique to the application, such as its name.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* activate()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Primary activation action, generally triggered via a left click.
* display(parentWindow, relativeX, relativeY)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  parentWindow: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)   relativeX: [int](https://doc.qt.io/qt-6/qml-int.html)   relativeY: [int](https://doc.qt.io/qt-6/qml-int.html)

  Display a platform menu at the given location relative to the parent window.
* scroll(delta, horizontal)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  delta: [int](https://doc.qt.io/qt-6/qml-int.html)   horizontal: [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Scroll action, such as changing volume on a mixer.
* secondaryActivate()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Secondary activation action, generally triggered via a middle click.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* ready()

  *No details provided*

* [menu](#menu)
* [status](#status)
* [tooltipDescription](#tooltipDescription)
* [icon](#icon)
* [onlyMenu](#onlyMenu)
* [category](#category)
* [title](#title)
* [tooltipTitle](#tooltipTitle)
* [hasMenu](#hasMenu)
* [id](#id)

* [activate](#activate)
* [display](#display)
* [scroll](#scroll)
* [secondaryActivate](#secondaryActivate)

* [ready](#ready)
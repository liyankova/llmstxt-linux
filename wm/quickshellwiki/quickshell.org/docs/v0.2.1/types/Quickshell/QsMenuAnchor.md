---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/QsMenuAnchor"
title: "Quickshell - QsMenuAnchor"
crawl_date: "2025-11-16T14:37:29.722022Z"
selector: ".docslayout"
---

# Quickshell - QsMenuAnchor

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [visible](#visible)
* [anchor](#anchor)
* [menu](#menu)

* [close](#close)
* [open](#open)

* [closed](#closed)
* [opened](#opened)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [QsMenuAnchor](/docs/v0.2.1/types/Quickshell/QsMenuAnchor)
 

---

## QsMenuAnchor: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell`

Display anchor for platform menus. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* visible  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the menu is currently open and visible.

  See also: [open()](#open), [close()](#close).
* anchor  : 
  [PopupAnchor](/docs/v0.2.1/types/Quickshell/PopupAnchor)

  readonly

  The menu’s anchor / positioner relative to another window. The menu will not be
  shown until it has a valid anchor.

  NOTE

  *The following is subject to change and NOT a guarantee of future behavior.*

  A snapshot of the anchor at the time [opened()](#opened) is emitted will be
  used to position the menu. Additional changes to the anchor after this point
  will not affect the placement of the menu.

  You can set properties of the anchor like so:

  ```
  QsMenuAnchor {
    anchor.window: parentwindow
    // or
    anchor {
      window: parentwindow
    }
  }
  ```
* menu  : 
  [QsMenuHandle](/docs/v0.2.1/types/Quickshell/QsMenuHandle)

  The menu that should be displayed on this anchor.

  See also: [SystemTrayItem.menu](/docs/v0.2.1/types/Quickshell.Services.SystemTray/SystemTrayItem#menu).

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* close()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Close the open menu.
* open()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Open the given menu on this menu Requires that [anchor](#anchor) is valid.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* closed()

  Sent when the menu is closed.
* opened()

  Sent when the menu is displayed onscreen which may be after [visible](#visible)
  becomes true.

* [visible](#visible)
* [anchor](#anchor)
* [menu](#menu)

* [close](#close)
* [open](#open)

* [closed](#closed)
* [opened](#opened)
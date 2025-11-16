---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/PopupWindow"
title: "Quickshell - PopupWindow"
crawl_date: "2025-11-16T14:37:26.203915Z"
selector: ".docslayout"
---

# Quickshell - PopupWindow

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [relativeY](#relativeY)
* [anchor](#anchor)
* [visible](#visible)
* [relativeX](#relativeX)
* [screen](#screen)
* [parentWindow](#parentWindow)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [PopupWindow](/docs/v0.2.1/types/Quickshell/PopupWindow)
 

---

## PopupWindow: [QsWindow](/docs/v0.2.1/types/Quickshell/QsWindow)

`import Quickshell`

Popup window that can display in a position relative to a floating
or panel window.

#### Example

The following snippet creates a panel with a popup centered over it.

```
PanelWindow {
  id: toplevel

  anchors {
    bottom: true
    left: true
    right: true
  }

  PopupWindow {
    anchor.window: toplevel
    anchor.rect.x: parentWindow.width / 2 - width / 2
    anchor.rect.y: parentWindow.height
    width: 500
    height: 500
    visible: true
  }
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* relativeY  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  > [!ERROR]
  > Deprecated in favor of `anchor.rect.y`.

  The Y position of the popup relative to the parent window.
* anchor  : 
  [PopupAnchor](/docs/v0.2.1/types/Quickshell/PopupAnchor)

  readonly

  The popup’s anchor / positioner relative to another item or window. The popup will
  not be shown until it has a valid anchor relative to a window and [visible](#visible) is true.

  You can set properties of the anchor like so:

  ```
  PopupWindow {
    anchor.window: parentwindow
    // or
    anchor {
      window: parentwindow
    }
  }
  ```
* visible  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the window is shown or hidden. Defaults to false.

  The popup will not be shown until [anchor](#anchor) is valid, regardless of this property.
* relativeX  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  > [!ERROR]
  > Deprecated in favor of `anchor.rect.x`.

  The X position of the popup relative to the parent window.
* screen  : 
  [ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)

  readonly

  The screen that the window currently occupies.

  This may be modified to move the window to the given screen.
* parentWindow  : 
  [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  > [!ERROR]
  > Deprecated in favor of `anchor.window`.

  The parent window of this popup.

  Changing this property reparents the popup.

* [relativeY](#relativeY)
* [anchor](#anchor)
* [visible](#visible)
* [relativeX](#relativeX)
* [screen](#screen)
* [parentWindow](#parentWindow)
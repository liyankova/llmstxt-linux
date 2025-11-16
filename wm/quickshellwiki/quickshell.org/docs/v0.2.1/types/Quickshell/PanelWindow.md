---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/PanelWindow"
title: "Quickshell - PanelWindow"
crawl_date: "2025-11-16T14:37:11.653766Z"
selector: ".docslayout"
---

# Quickshell - PanelWindow

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [aboveWindows](#aboveWindows)
* [anchors](#anchors)
* [exclusionMode](#exclusionMode)
* [exclusiveZone](#exclusiveZone)
* [focusable](#focusable)
* [margins](#margins)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [PanelWindow](/docs/v0.2.1/types/Quickshell/PanelWindow)
 

---

## PanelWindow: [QsWindow](/docs/v0.2.1/types/Quickshell/QsWindow)

`import Quickshell`

Decorationless window attached to screen edges by anchors.

#### Example

The following snippet creates a white bar attached to the bottom of the screen.

```
PanelWindow {
  anchors {
    left: true
    bottom: true
    right: true
  }

  Text {
    anchors.centerIn: parent
    text: "Hello!"
  }
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* aboveWindows  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the panel should render above standard windows. Defaults to true.

  Note: On Wayland this property corrosponds to [WlrLayershell.layer](/docs/v0.2.1/types/Quickshell.Wayland/WlrLayershell#layer).
* anchors  : 
  [[bottom,top,left,right]](#)

  bottom:[bool](https://doc.qt.io/qt-6/qml-bool.html)   top:[bool](https://doc.qt.io/qt-6/qml-bool.html)   left:[bool](https://doc.qt.io/qt-6/qml-bool.html)   right:[bool](https://doc.qt.io/qt-6/qml-bool.html)

  Anchors attach a shell window to the sides of the screen.
  By default all anchors are disabled to avoid blocking the entire screen due to a misconfiguration.

  NOTE

  When two opposite anchors are attached at the same time, the corrosponding dimension
  (width or height) will be forced to equal the screen width/height.
  Margins can be used to create anchored windows that are also disconnected from the monitor sides.
* exclusionMode  : 
  [ExclusionMode](/docs/v0.2.1/types/Quickshell/ExclusionMode)

  Defaults to `ExclusionMode.Auto`.
* exclusiveZone  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  The amount of space reserved for the shell layer relative to its anchors.
  Setting this property sets [exclusionMode](#exclusionMode) to `ExclusionMode.Normal`.

  NOTE

  Either 1 or 3 anchors are required for the zone to take effect.
* focusable  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the panel should accept keyboard focus. Defaults to false.

  Note: On Wayland this property corrosponds to [WlrLayershell.keyboardFocus](/docs/v0.2.1/types/Quickshell.Wayland/WlrLayershell#keyboardFocus).
* margins  : 
  [[right,top,bottom,left]](#)

  right:[int](https://doc.qt.io/qt-6/qml-int.html)   top:[int](https://doc.qt.io/qt-6/qml-int.html)   bottom:[int](https://doc.qt.io/qt-6/qml-int.html)   left:[int](https://doc.qt.io/qt-6/qml-int.html)

  Offsets from the sides of the screen.

  NOTE

  Only applies to edges with anchors

* [aboveWindows](#aboveWindows)
* [anchors](#anchors)
* [exclusionMode](#exclusionMode)
* [exclusiveZone](#exclusiveZone)
* [focusable](#focusable)
* [margins](#margins)
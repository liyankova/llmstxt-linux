---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Wayland/WlrLayershell"
title: "Quickshell.Wayland - WlrLayershell"
crawl_date: "2025-11-16T14:42:33.597599Z"
selector: ".docslayout"
---

# Quickshell.Wayland - WlrLayershell

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [namespace](#namespace)
* [keyboardFocus](#keyboardFocus)
* [layer](#layer)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Wayland](/docs/v0.2.1/types/Quickshell.Wayland)
6. [WlrLayershell](/docs/v0.2.1/types/Quickshell.Wayland/WlrLayershell)
 

---

## WlrLayershell: [PanelWindow](/docs/v0.2.1/types/Quickshell/PanelWindow)

`import Quickshell.Wayland`

Decorationless window that can be attached to the screen edges using the [zwlr\_layer\_shell\_v1](https://wayland.app/protocols/wlr-layer-shell-unstable-v1) protocol.

#### Attached object

`WlrLayershell` works as an attached object of [PanelWindow](/docs/v0.2.1/types/Quickshell/PanelWindow) which you should use instead if you can,
as it is platform independent.

```
PanelWindow {
  // When PanelWindow is backed with WlrLayershell this will work
  WlrLayershell.layer: WlrLayer.Bottom
}
```

To maintain platform compatibility you can dynamically set layershell specific properties.

```
PanelWindow {
  Component.onCompleted: {
    if (this.WlrLayershell != null) {
      this.WlrLayershell.layer = WlrLayer.Bottom;
    }
  }
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* namespace  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Similar to the class property of windows. Can be used to identify the window to external tools.

  Cannot be set after windowConnected.
* keyboardFocus  : 
  [WlrKeyboardFocus](/docs/v0.2.1/types/Quickshell.Wayland/WlrKeyboardFocus)

  The degree of keyboard focus taken. Defaults to `KeyboardFocus.None`.
* layer  : 
  [WlrLayer](/docs/v0.2.1/types/Quickshell.Wayland/WlrLayer)

  The shell layer the window sits in. Defaults to `WlrLayer.Top`.

* [namespace](#namespace)
* [keyboardFocus](#keyboardFocus)
* [layer](#layer)
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Wayland/ToplevelManager"
title: "Quickshell.Wayland - ToplevelManager"
crawl_date: "2025-11-16T14:42:19.480685Z"
selector: ".docslayout"
---

# Quickshell.Wayland - ToplevelManager

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [activeToplevel](#activeToplevel)
* [toplevels](#toplevels)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Wayland](/docs/v0.2.1/types/Quickshell.Wayland)
6. [ToplevelManager](/docs/v0.2.1/types/Quickshell.Wayland/ToplevelManager)
 

---

## ToplevelManager: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell.Wayland`

Exposes a list of windows from other applications as [Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel)s via the
[zwlr-foreign-toplevel-management-v1](https://wayland.app/protocols/wlr-foreign-toplevel-management-unstable-v1)
wayland protocol.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* activeToplevel  : 
  [Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel)

  readonly

  Active toplevel or null.

  NOTE

  If multiple are active, this will be the most recently activated one.
  Usually compositors will not report more than one toplevel as active at a time.
* toplevels  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel)>

  readonly

  All toplevel windows exposed by the compositor.

* [activeToplevel](#activeToplevel)
* [toplevels](#toplevels)
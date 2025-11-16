---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandWorkspace"
title: "Quickshell.Hyprland - HyprlandWorkspace"
crawl_date: "2025-11-16T14:39:18.753938Z"
selector: ".docslayout"
---

# Quickshell.Hyprland - HyprlandWorkspace

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [id](#id)
* [toplevels](#toplevels)
* [lastIpcObject](#lastIpcObject)
* [name](#name)
* [hasFullscreen](#hasFullscreen)
* [focused](#focused)
* [active](#active)
* [urgent](#urgent)
* [monitor](#monitor)

* [activate](#activate)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Hyprland](/docs/v0.2.1/types/Quickshell.Hyprland)
6. [HyprlandWorkspace](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandWorkspace)
 

---

## HyprlandWorkspace: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Hyprland`

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* id  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  *No details provided*
* toplevels  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel)

  readonly

  List of toplevels on this workspace.
* lastIpcObject  : 
  [unknown](#unknown)

  readonly

  Last json returned for this workspace, as a javascript object.

  WARNING

  This is *not* updated unless the workspace object is fetched again from
  Hyprland. If you need a value that is subject to change and does not have a dedicated
  property, run [Hyprland.refreshWorkspaces()](/docs/v0.2.1/types/Quickshell.Hyprland/Hyprland#refreshWorkspaces) and wait for this property to update.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* hasFullscreen  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this workspace currently has a fullscreen client.
* focused  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this workspace is currently active on a monitor and that monitor is currently
  focused. See also [active](#active).
* active  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this workspace is currently active on its monitor. See also [focused](#focused).
* urgent  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this workspace has a window that is urgent.
  Becomes always falsed after the workspace is [focused](#focused).
* monitor  : 
  [HyprlandMonitor](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandMonitor)

  readonly

  *No details provided*

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* activate()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Activate the workspace.

  NOTE

  This is equivalent to running

  ```
  HyprlandIpc.dispatch(`workspace ${workspace.name}`);
  ```

* [id](#id)
* [toplevels](#toplevels)
* [lastIpcObject](#lastIpcObject)
* [name](#name)
* [hasFullscreen](#hasFullscreen)
* [focused](#focused)
* [active](#active)
* [urgent](#urgent)
* [monitor](#monitor)

* [activate](#activate)
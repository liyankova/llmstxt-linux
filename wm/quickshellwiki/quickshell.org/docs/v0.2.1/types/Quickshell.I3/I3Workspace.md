---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.I3/I3Workspace"
title: "Quickshell.I3 - I3Workspace"
crawl_date: "2025-11-16T14:39:31.696122Z"
selector: ".docslayout"
---

# Quickshell.I3 - I3Workspace

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [id](#id)
* [focused](#focused)
* [name](#name)
* [num](#num)
* [monitor](#monitor)
* [urgent](#urgent)
* [active](#active)
* [number](#number)
* [lastIpcObject](#lastIpcObject)

* [activate](#activate)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.I3](/docs/v0.2.1/types/Quickshell.I3)
6. [I3Workspace](/docs/v0.2.1/types/Quickshell.I3/I3Workspace)
 

---

## I3Workspace: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.I3`

I3/Sway workspaces 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* id  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The ID of this workspace, it is unique for i3/Sway launch
* focused  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this workspace is currently active on a monitor and that monitor is currently
  focused. See also [active](#active).
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The name of this workspace
* num  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  Deprecated: use [number](#number)
* monitor  : 
  [I3Monitor](/docs/v0.2.1/types/Quickshell.I3/I3Monitor)

  readonly

  The monitor this workspace is being displayed on
* urgent  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If a window in this workspace has an urgent notification
* active  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this workspace is currently active on its monitor. See also [focused](#focused).
* number  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The number of this workspace
* lastIpcObject  : 
  [unknown](#unknown)

  readonly

  Last JSON returned for this workspace, as a JavaScript object.

  This updates every time we receive a `workspace` event from i3/Sway

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* activate()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Activate the workspace.

  NOTE

  This is equivalent to running

  ```
  I3.dispatch(`workspace number ${workspace.number}`);
  ```

* [id](#id)
* [focused](#focused)
* [name](#name)
* [num](#num)
* [monitor](#monitor)
* [urgent](#urgent)
* [active](#active)
* [number](#number)
* [lastIpcObject](#lastIpcObject)

* [activate](#activate)
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandToplevel"
title: "Quickshell.Hyprland - HyprlandToplevel"
crawl_date: "2025-11-16T14:39:09.672137Z"
selector: ".docslayout"
---

# Quickshell.Hyprland - HyprlandToplevel

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [address](#address)
* [title](#title)
* [activated](#activated)
* [wayland](#wayland)
* [handle](#handle)
* [workspace](#workspace)
* [lastIpcObject](#lastIpcObject)
* [urgent](#urgent)
* [monitor](#monitor)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Hyprland](/docs/v0.2.1/types/Quickshell.Hyprland)
6. [HyprlandToplevel](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandToplevel)
 

---

## HyprlandToplevel: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Hyprland`

Represents a window as Hyprland exposes it.
Can also be used as an attached object of a [Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel),
to resolve a handle to an Hyprland toplevel.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* address  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Hexadecimal Hyprland window address. Will be an empty string until
  the address is reported.
* title  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The title of the toplevel
* activated  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  Whether the toplevel is active or not
* wayland  : 
  [Toplevel](/docs/v0.2.1/types/Quickshell.Wayland/Toplevel)

  readonly

  The wayland toplevel handle. Will be null intil the address is reported
* handle  : 
  [HyprlandToplevel](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandToplevel)

  readonly

  The toplevel handle, exposing the Hyprland toplevel.
  Will be null until the address is reported
* workspace  : 
  [HyprlandWorkspace](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandWorkspace)

  readonly

  The current workspace of the toplevel (might be null)
* lastIpcObject  : 
  [unknown](#unknown)

  readonly

  Last json returned for this toplevel, as a javascript object.

  WARNING

  This is *not* updated unless the toplevel object is fetched again from
  Hyprland. If you need a value that is subject to change and does not have a dedicated
  property, run [Hyprland.refreshToplevels()](/docs/v0.2.1/types/Quickshell.Hyprland/Hyprland#refreshToplevels) and wait for this property to update.
* urgent  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  Whether the client is urgent or not
* monitor  : 
  [HyprlandMonitor](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandMonitor)

  readonly

  The current monitor of the toplevel (might be null)

* [address](#address)
* [title](#title)
* [activated](#activated)
* [wayland](#wayland)
* [handle](#handle)
* [workspace](#workspace)
* [lastIpcObject](#lastIpcObject)
* [urgent](#urgent)
* [monitor](#monitor)
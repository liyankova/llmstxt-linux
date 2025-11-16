---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandEvent"
title: "Quickshell.Hyprland - HyprlandEvent"
crawl_date: "2025-11-16T14:39:00.937610Z"
selector: ".docslayout"
---

# Quickshell.Hyprland - HyprlandEvent

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [data](#data)
* [name](#name)

* [parse](#parse)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Hyprland](/docs/v0.2.1/types/Quickshell.Hyprland)
6. [HyprlandEvent](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandEvent)
 

---

## HyprlandEvent: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Hyprland`

Live Hyprland IPC event. Holding this object after the
signal handler exits is undefined as the event instance
is reused.

Emitted by [Hyprland.rawEvent()](/docs/v0.2.1/types/Quickshell.Hyprland/Hyprland#rawEvent).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* data  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The unparsed data of the event.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The name of the event.

  See [Hyprland Wiki: IPC](https://wiki.hyprland.org/IPC/) for a list of events.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* parse(argumentCount)  : 
  [list](https://doc.qt.io/qt-6/qml-list.html)

  argumentCount: [int](https://doc.qt.io/qt-6/qml-int.html)

  Parse this event with a known number of arguments.

  Argument count is required as some events can contain commas
  in the last argument, which can be ignored as long as the count is known.

* [data](#data)
* [name](#name)

* [parse](#parse)
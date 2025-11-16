---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Hyprland/Hyprland"
title: "Quickshell.Hyprland - Hyprland"
crawl_date: "2025-11-16T14:38:57.710491Z"
selector: ".docslayout"
---

# Quickshell.Hyprland - Hyprland

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [focusedWorkspace](#focusedWorkspace)
* [monitors](#monitors)
* [eventSocketPath](#eventSocketPath)
* [activeToplevel](#activeToplevel)
* [toplevels](#toplevels)
* [workspaces](#workspaces)
* [focusedMonitor](#focusedMonitor)
* [requestSocketPath](#requestSocketPath)

* [dispatch](#dispatch)
* [monitorFor](#monitorFor)
* [refreshMonitors](#refreshMonitors)
* [refreshToplevels](#refreshToplevels)
* [refreshWorkspaces](#refreshWorkspaces)

* [rawEvent](#rawEvent)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Hyprland](/docs/v0.2.1/types/Quickshell.Hyprland)
6. [Hyprland](/docs/v0.2.1/types/Quickshell.Hyprland/Hyprland)
 

---

## Hyprland: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell.Hyprland`

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* focusedWorkspace  : 
  [HyprlandWorkspace](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandWorkspace)

  readonly

  The currently focused hyprland workspace. May be null.
* monitors  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[HyprlandMonitor](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandMonitor)>

  readonly

  All hyprland monitors.
* eventSocketPath  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Path to the event socket (.socket2.sock)
* activeToplevel  : 
  [HyprlandToplevel](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandToplevel)

  readonly

  Currently active toplevel (might be null)
* toplevels  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[HyprlandToplevel](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandToplevel)>

  readonly

  All hyprland toplevels
* workspaces  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[HyprlandWorkspace](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandWorkspace)>

  readonly

  All hyprland workspaces, sorted by id.

  NOTE

  Named workspaces have a negative id, and will appear before unnamed workspaces.
* focusedMonitor  : 
  [HyprlandMonitor](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandMonitor)

  readonly

  The currently focused hyprland monitor. May be null.
* requestSocketPath  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Path to the request socket (.socket.sock)

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* dispatch(request)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  request: [string](https://doc.qt.io/qt-6/qml-string.html)

  Execute a hyprland [dispatcher](https://wiki.hyprland.org/Configuring/Dispatchers).
* monitorFor(screen)  : 
  [HyprlandMonitor](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandMonitor)

  screen: [ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)

  Get the HyprlandMonitor object that corrosponds to a quickshell screen.
* refreshMonitors()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Refresh monitor information.

  Many actions that will invalidate monitor state don’t send events,
  so this function is available if required.
* refreshToplevels()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Refresh toplevel information.

  Many actions that will invalidate workspace state don’t send events,
  so this function is available if required.
* refreshWorkspaces()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Refresh workspace information.

  Many actions that will invalidate workspace state don’t send events,
  so this function is available if required.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* rawEvent(event)

  event: [HyprlandEvent](/docs/v0.2.1/types/Quickshell.Hyprland/HyprlandEvent)

  Emitted for every event that comes in through the hyprland event socket (socket2).

  See [Hyprland Wiki: IPC](https://wiki.hyprland.org/IPC/) for a list of events.

* [focusedWorkspace](#focusedWorkspace)
* [monitors](#monitors)
* [eventSocketPath](#eventSocketPath)
* [activeToplevel](#activeToplevel)
* [toplevels](#toplevels)
* [workspaces](#workspaces)
* [focusedMonitor](#focusedMonitor)
* [requestSocketPath](#requestSocketPath)

* [dispatch](#dispatch)
* [monitorFor](#monitorFor)
* [refreshMonitors](#refreshMonitors)
* [refreshToplevels](#refreshToplevels)
* [refreshWorkspaces](#refreshWorkspaces)

* [rawEvent](#rawEvent)
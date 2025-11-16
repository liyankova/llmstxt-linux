---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.DBusMenu/DBusMenuItem"
title: "Quickshell.DBusMenu - DBusMenuItem"
crawl_date: "2025-11-16T14:38:51.576344Z"
selector: ".docslayout"
---

# Quickshell.DBusMenu - DBusMenuItem

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [menuHandle](#menuHandle)

* [updateLayout](#updateLayout)

* [layoutUpdated](#layoutUpdated)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.DBusMenu](/docs/v0.2.1/types/Quickshell.DBusMenu)
6. [DBusMenuItem](/docs/v0.2.1/types/Quickshell.DBusMenu/DBusMenuItem)
 

---

## DBusMenuItem: [QsMenuEntry](/docs/v0.2.1/types/Quickshell/QsMenuEntry)

uncreatable

`import Quickshell.DBusMenu`

Menu item shared by an external program via the
[DBusMenu specification](https://github.com/AyatanaIndicators/libdbusmenu/blob/master/libdbusmenu-glib/dbus-menu.xml).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* menuHandle  : 
  [DBusMenuHandle](/docs/v0.2.1/types/Quickshell.DBusMenu/DBusMenuHandle)

  readonly

  Handle to the root of this menu.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* updateLayout()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Refreshes the menu contents.

  Usually you shouldn’t need to call this manually but some applications providing
  menus do not update them correctly. Call this if menus don’t update their state.

  The [layoutUpdated()](#layoutUpdated) signal will be sent when a response is received.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* layoutUpdated()

  *No details provided*

* [menuHandle](#menuHandle)

* [updateLayout](#updateLayout)

* [layoutUpdated](#layoutUpdated)
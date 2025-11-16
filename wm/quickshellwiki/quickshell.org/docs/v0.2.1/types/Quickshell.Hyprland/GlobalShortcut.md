---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Hyprland/GlobalShortcut"
title: "Quickshell.Hyprland - GlobalShortcut"
crawl_date: "2025-11-16T14:38:54.542013Z"
selector: ".docslayout"
---

# Quickshell.Hyprland - GlobalShortcut

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [pressed](#pressed)
* [triggerDescription](#triggerDescription)
* [description](#description)
* [name](#name)
* [appid](#appid)

* [released](#released)
* [pressed](#pressed)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Hyprland](/docs/v0.2.1/types/Quickshell.Hyprland)
6. [GlobalShortcut](/docs/v0.2.1/types/Quickshell.Hyprland/GlobalShortcut)
 

---

## GlobalShortcut: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell.Hyprland`

Global shortcut implemented with [hyprland\_global\_shortcuts\_v1](https://github.com/hyprwm/hyprland-protocols/blob/main/protocols/hyprland-global-shortcuts-v1.xml).

You can use this within hyprland as a global shortcut:

```
bind = <modifiers>, <key>, global, <appid>:<name>
```

See [the wiki](https://wiki.hyprland.org/Configuring/Binds/#dbus-global-shortcuts) for details.

WARNING

The shortcuts protocol does not allow duplicate appid + name pairs.
Within a single instance of quickshell this is handled internally, and both
users will be notified, but multiple instances of quickshell or XDPH may collide.

If that happens, whichever client that tries to register the shortcuts last will crash.

NOTE

This type does *not* use the xdg-desktop-portal global shortcuts protocol,
as it is not fully functional without flatpak and would cause a considerably worse
user experience from other limitations. It will only work with Hyprland.
Note that, as this type bypasses xdg-desktop-portal, XDPH is not required.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* pressed  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the keybind is currently pressed.
* triggerDescription  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Have not seen this used ever, but included for completeness. Safe to ignore.
* description  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The description of the shortcut that appears in `hyprctl globalshortcuts`.
  You cannot change this at runtime.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The name of the shortcut.
  You cannot change this at runtime.
* appid  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The appid of the shortcut. Defaults to `quickshell`.
  You cannot change this at runtime.

  If you have more than one shortcut we recommend subclassing
  GlobalShortcut to set this.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* released()

  Fired when the keybind is released.
* pressed()

  Fired when the keybind is pressed.

* [pressed](#pressed)
* [triggerDescription](#triggerDescription)
* [description](#description)
* [name](#name)
* [appid](#appid)

* [released](#released)
* [pressed](#pressed)
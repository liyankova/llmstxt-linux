---
source_url: "https://quickshell.org/about"
title: "About Quickshell"
crawl_date: "2025-11-16T14:36:16.401592Z"
selector: ".docslayout"
---

# About Quickshell

### [Quickshell](/)

`CtrlK`   

Cancel

  

About Quickshell

---

- [Is Quickshell for me?](#is-quickshell-for-me)
  * [I want a preconfigured desktop](#i-want-a-preconfigured-desktop)
  * [I want to make my own](#i-want-to-make-my-own)

2. [About](/about)
 

---

# About Quickshell

Quickshell is a toolkit for building a desktop shell, which is to say components
of your desktop like bars, widgets, lock screens, display managers, and the like.

Quickshell is based on QtQuick and configured with QML, the QtQuick interface
description language. It provides integrations for common shell functionality,
as well as support for hot reloading and tools to work with processes,
sockets, files, and more.

Built-in integrations are currently provided for:

* Wayland and X11 for windowing
* Wayland for window management and screen recording
* Workspace management in Hyprland, I3, and Sway
* Pipewire for audio controls
* BlueZ for bluetooth
* Pam for authentication and building lockscreens
* Greetd for building a display manager
* UPower for monitoring battery statistics
* Power Profiles Daemon
* MPRIS compatible media players
* StatusNotifierItem compatible system tray clients

## Is Quickshell for me?

#### I want a preconfigured desktop

There are many setups intended to be useful without much tweaking, for example:

* [Caelestia](https://github.com/caelestia-dots/shell) by Soramane
* [Illogical-Impulse](https://github.com/end-4/dots-hyprland) by end\_4.

#### I want to make my own

Quickshell is a relatively low-level tool compared to simple status bars like Waybar.
When writing a Quickshell configuration, you are not just changing styles and layouts, but
practically programming, which is considerably more complex.

You can see the [QML Language Reference](/docs/guide/qml-language) to get an idea
of what you’re getting into.

NEXT STEPS

See the [Usage Guide](/docs/guide) to learn how to set up and use Quickshell.

About Quickshell

---

- [Is Quickshell for me?](#is-quickshell-for-me)
  * [I want a preconfigured desktop](#i-want-a-preconfigured-desktop)
  * [I want to make my own](#i-want-to-make-my-own)
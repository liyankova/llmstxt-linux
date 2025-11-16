---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Wayland/WlrKeyboardFocus"
title: "Quickshell.Wayland - WlrKeyboardFocus"
crawl_date: "2025-11-16T14:42:27.985614Z"
selector: ".docslayout"
---

# Quickshell.Wayland - WlrKeyboardFocus

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [OnDemand](#OnDemand)
* [None](#None)
* [Exclusive](#Exclusive)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Wayland](/docs/v0.2.1/types/Quickshell.Wayland)
6. [WlrKeyboardFocus](/docs/v0.2.1/types/Quickshell.Wayland/WlrKeyboardFocus)
 

---

## WlrKeyboardFocus: WlrKeyboardFocus

`import Quickshell.Wayland`

See [WlrLayershell.keyboardFocus](/docs/v0.2.1/types/Quickshell.Wayland/WlrLayershell#keyboardFocus).

 

## Variants

* OnDemand

  Access to the keyboard as determined by the operating system.

  WARNING

  On some systems, `OnDemand` may cause the shell window to
  retain focus over another window unexpectedly.
  You should try `None` if you experience issues.
* None

  No keyboard input will be accepted.
* Exclusive

  Exclusive access to the keyboard, locking out all other windows.

  WARNING

  You **CANNOT** use this to make a secure lock screen.

  If you want to make a lock screen, use [WlSessionLock](/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLock).

* [OnDemand](#OnDemand)
* [None](#None)
* [Exclusive](#Exclusive)
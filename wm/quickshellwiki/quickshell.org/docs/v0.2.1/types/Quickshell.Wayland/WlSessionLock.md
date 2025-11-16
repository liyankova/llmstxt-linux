---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLock"
title: "Quickshell.Wayland - WlSessionLock"
crawl_date: "2025-11-16T14:42:22.143101Z"
selector: ".docslayout"
---

# Quickshell.Wayland - WlSessionLock

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [locked](#locked)
* [secure](#secure)
* [surface](#surface)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Wayland](/docs/v0.2.1/types/Quickshell.Wayland)
6. [WlSessionLock](/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLock)
 

---

## WlSessionLock: [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)

`import Quickshell.Wayland`

Wayland session lock implemented using the [ext\_session\_lock\_v1](https://wayland.app/protocols/ext-session-lock-v1) protocol.

WlSessionLock will create an instance of its `surface` component for every screen when
`locked` is set to true. The `surface` component must create a [WlSessionLockSurface](/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLockSurface)
which will be displayed on each screen.

The below example will create a session lock that disappears when the button is clicked.

```
WlSessionLock {
  id: lock

  WlSessionLockSurface {
    Button {
      text: "unlock me"
      onClicked: lock.locked = false
    }
  }
}

// ...
lock.locked = true
```

WARNING

If the WlSessionLock is destroyed or quickshell exits without setting `locked`
to false, conformant compositors will leave the screen locked and painted with a solid
color.

This is what makes the session lock secure. The lock dying will not expose your session,
but it will render it inoperable.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* locked  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Controls the lock state.

  WARNING

  Only one WlSessionLock may be locked at a time. Attempting to enable a lock while
  another lock is enabled will do nothing.
* secure  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  The compositor lock state.

  This is set to true once the compositor has confirmed all screens are covered with locks.
* surface  : 
  [Component](https://doc.qt.io/qt-6/qml-qtqml-component.html)

  default

  The surface that will be created for each screen. Must create a [WlSessionLockSurface](/docs/v0.2.1/types/Quickshell.Wayland/WlSessionLockSurface).

* [locked](#locked)
* [secure](#secure)
* [surface](#surface)
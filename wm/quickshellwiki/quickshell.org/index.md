---
source_url: "https://quickshell.org/"
title: "Quickshell"
crawl_date: "2025-11-16T14:35:25.211366Z"
selector: "body"
---

# Quickshell

[Quickshell 0.2.1 has been released! | 2025-10-11](/changelog)

![Quickshell](/favicon.svg)

# Quickshell

## building blocks for your desktop

[  ](/assets/showcase/soramane.mp4)

Configuration by [soramane](https://github.com/soramanew) ([install](https://github.com/caelestia-dots/shell))

[  ](/assets/showcase/end4.mp4)

Configuration by [end\_4](https://github.com/end-4) ([install](https://github.com/end-4/dots-hyprland))

[  ](/assets/showcase/outfoxxed.mp4)

Configuration by [outfoxxed](https://outfoxxed.me) ([source code](https://git.outfoxxed.me/outfoxxed/nixnew/src/branch/master/modules/user/modules/quickshell))

[  ](/assets/showcase/pfaj-bdeblase.mp4)

Configuration by [pfaj](https://github.com/pfaj/) and [bdebiase](https://github.com/bdebiase)

[  ](/assets/showcase/flicko.mp4)

Configuration by [flicko](https://github.com/flickowoa) ([source code](https://github.com/flickowoa/zephyr))

[  ](/assets/showcase/vaxry.mp4)

Configuration by [vaxry](https://vaxry.net)

Quickshell is a toolkit for building status bars, widgets, lockscreens,
and other desktop components using QtQuick. It can be used alongside your
wayland compositor or window manager to build a complete desktop environment.
  
   
 [More information](/about)

[### Install](/docs/v0.2.1/guide/install-setup) [### Documentation](/docs/v0.2.1/types)

* ### See your changes in real time

  Quickshell loads changes as soon as they're saved, letting you iterate as fast as you can type.

  [  ](/assets/simple-shell-livereload.mp4)
* ### Easy to use language

  Quickshell is configured in QML, a simple language designed for creating flexible user interfaces.
  It also has LSP support.

  ```
  // a standard desktop window
  FloatingWindow {
    Timer {
      // assign an id to the object, which can be
      // used to reference it
      id: timer
      property bool invert: false // a custom property

      // change the value of invert every half second
      running: true; repeat: true
      interval: 500 // ms
      onTriggered: timer.invert = !timer.invert
    }

    // change the window's color when timer.invert changes
    color: timer.invert ? "purple" : "green"
  }
  ```

  ```
  // a standard desktop window
  FloatingWindow {
    Timer {
      // assign an id to the
      // object, which can be
      // used to reference it
      id: timer
      // a custom property
      property bool invert: false

      // change the value of invert
      // every half second
      running: true; repeat: true
      interval: 500 // ms
      onTriggered: {
        timer.invert = !timer.invert
      }
    }

    // change the window's color
    // when timer.invert changes
    color: timer.invert
      ? "purple"
      : "green"
  }
  ```
* ### Extensive integrations

  Quickshell comes with a large set of integrations, with new ones arriving all the time.

  ![Quickshell](/favicon.svg)

  ![Wayland](/assets/logos/wayland.svg)

   

  ![Hyprland](/assets/logos/hyprland.svg)

   

  ![Pipewire](/assets/logos/pipewire.svg)

   

  ![X.Org](/assets/logos/xorg.svg)

   

  ![Sway](/assets/logos/sway.svg)
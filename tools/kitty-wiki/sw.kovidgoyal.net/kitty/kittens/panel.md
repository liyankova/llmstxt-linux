---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/panel/"
title: "Draw a GPU accelerated dock panel on your desktop - kitty"
crawl_date: "2025-11-16T14:48:29.725011Z"
selector: "article"
---

# Draw a GPU accelerated dock panel on your desktop - kitty

# Draw a GPU accelerated dock panel on your desktop[¶](#draw-a-gpu-accelerated-dock-panel-on-your-desktop "Link to this heading")

Draw the desktop wallpaper or docks and panels using arbitrary
terminal programs, For example, have [btop](https://github.com/aristocratos/btop) or [cava](https://github.com/karlstav/cava/) be your desktop wallpaper.

It is useful for showing status information or notifications on your desktop
using terminal programs instead of GUI toolkits.

The screenshot to the side shows some uses of the panel kitten to draw various
desktop components such as the background, a quick access floating terminal and
a dock panel showing system information (Linux only).

Added in version 0.42.0: Support for macOS, see [compatibility matrix](#panel-compat) for details.
and X11 (background and overlay).

Added in version 0.34.0: Support for Wayland. See [below](#panel-compat) for which
Wayland compositors work.

Using this kitten is simple, for example:

```
kitten panel sh -c 'printf "\n\n\nHello, world."; sleep 5s'
```

This will show `Hello, world.` at the top edge of your screen for five
seconds. Here, the terminal program we are running is **sh** with a script
to print out `Hello, world!`. You can make the terminal program as complex as
you like, as demonstrated in the screenshots.

If you are on Wayland or macOS, you can, for instance, run:

```
kitten panel --edge=background htop
```

to display `htop` as your desktop background. Remember this works in everything
but GNOME and also, in sway, you have to disable the background wallpaper as
sway renders that over the panel kitten surface.

There are projects that make use of this facility to implement generalised
panels and desktop components:

> * [kitty panel](https://github.com/5hubham5ingh/kitty-panel)
> * [pawbar](https://github.com/codelif/pawbar)

## Controlling panels via remote control[¶](#controlling-panels-via-remote-control "Link to this heading")

You can control panels via the kitty [remote control](../../remote-control/) facility. Create a panel
with remote control enabled:

```
kitten panel -o allow_remote_control=socket-only --lines=2 \
    --listen-on=unix:/tmp/panel kitten run-shell
```

Now you can control this panel using remote control, for example to show/hide
it, use:

```
kitten @ --to=unix:/tmp/panel resize-os-window --action=toggle-visibility
```

To move the panel to the bottom of the screen and increase its height:

```
kitten @ --to=unix:/tmp/panel resize-os-window --action=os-panel \
    --incremental edge=bottom lines=4
```

To create a new panel running the program top, in the same instance
(like creating a new OS window):

```
kitten @ --to=unix:/tmp/panel launch --type=os-panel --os-panel edge=top \
    --os-panel lines=8 top
```

### Source code for panel[¶](#source-code-for-panel "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/panel).

### Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitty +kitten panel [options] [cmdline-to-run ...]
```

Use a command line program to draw a GPU accelerated panel on your desktop

## Options[¶](#options "Link to this heading")

--lines <LINES>[¶](#cmdoption-kitty-kitten-panel-lines "Link to this definition")
:   The number of lines shown in the panel. Ignored for background, centered, and vertical panels. If it has the suffix `px` then it sets the height of the panel in pixels instead of lines.
    Default: `1`

--columns <COLUMNS>[¶](#cmdoption-kitty-kitten-panel-columns "Link to this definition")
:   The number of columns shown in the panel. Ignored for background, centered, and horizontal panels. If it has the suffix `px` then it sets the width of the panel in pixels instead of columns.
    Default: `1`

--margin-top <MARGIN\_TOP>[¶](#cmdoption-kitty-kitten-panel-margin-top "Link to this definition")
:   Set the top margin for the panel, in pixels. Has no effect for bottom edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.
    Default: `0`

--margin-left <MARGIN\_LEFT>[¶](#cmdoption-kitty-kitten-panel-margin-left "Link to this definition")
:   Set the left margin for the panel, in pixels. Has no effect for right edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.
    Default: `0`

--margin-bottom <MARGIN\_BOTTOM>[¶](#cmdoption-kitty-kitten-panel-margin-bottom "Link to this definition")
:   Set the bottom margin for the panel, in pixels. Has no effect for top edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.
    Default: `0`

--margin-right <MARGIN\_RIGHT>[¶](#cmdoption-kitty-kitten-panel-margin-right "Link to this definition")
:   Set the right margin for the panel, in pixels. Has no effect for left edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.
    Default: `0`

--edge <EDGE>[¶](#cmdoption-kitty-kitten-panel-edge "Link to this definition")
:   Which edge of the screen to place the panel on. Note that some window managers (such as i3) do not support placing docked windows on the left and right edges. The value `background` means make the panel the “desktop wallpaper”. Note that when using sway if you set a background in your sway config it will cover the background drawn using this kitten. Additionally, there are three more values: `center`, `center-sized` and `none`. The value `center` anchors the panel to all sides and covers the entire display (on macOS the part of the display not covered by titlebar and dock). The panel can be shrunk and placed using the margin parameters. The value `none` anchors the panel to the top left corner and should be placed using the margin parameters. Its size is set by [`--lines`](#cmdoption-kitty-kitten-panel-lines) and [`--columns`](#cmdoption-kitty-kitten-panel-columns). The value `center-sized` is just like `none` except that the panel is centered instead of in the top left corner and the margins have no effect.
    Default: `top`
    Choices: `background`, `bottom`, `center`, `center-sized`, `left`, `none`, `right`, `top`

--layer <LAYER>[¶](#cmdoption-kitty-kitten-panel-layer "Link to this definition")
:   On a Wayland compositor that supports the wlr layer shell protocol, specifies the layer on which the panel should be drawn. This parameter is ignored and set to `background` if [`--edge`](#cmdoption-kitty-kitten-panel-edge) is set to `background`. On macOS, maps these to appropriate NSWindow *levels*.
    Default: `bottom`
    Choices: `background`, `bottom`, `overlay`, `top`

--config <CONFIG>, -c <CONFIG>[¶](#cmdoption-kitty-kitten-panel-config "Link to this definition")
:   Path to config file to use for kitty when drawing the panel.

--override <OVERRIDE>, -o <OVERRIDE>[¶](#cmdoption-kitty-kitten-panel-override "Link to this definition")
:   default= Override individual kitty configuration options, can be specified multiple times. Syntax: name=value. For example: [`kitty +kitten panel -o`](#cmdoption-kitty-kitten-panel-override) font\_size=20

--output-name <OUTPUT\_NAME>[¶](#cmdoption-kitty-kitten-panel-output-name "Link to this definition")
:   The panel can only be displayed on a single monitor (output) at a time. This allows you to specify which output is used, by name. If not specified the compositor will choose an output automatically, typically the last output the user interacted with or the primary monitor. Use the special value `list` to get a list of available outputs. Use `listjson` for a json encoded output. Note that on Wayland the output can only be set at panel creation time, it cannot be changed after creation, nor is there anyway to display a single panel on all outputs. Please complain to the Wayland developers about this.

--app-id <CLS>, --class <CLS>[¶](#cmdoption-kitty-kitten-panel-app-id "Link to this definition")
:   On Wayland set the namespace of the layer shell surface. On X11 set the class part of the WM\_CLASS window property.
    Default: `kitty-panel`

--name <NAME>, --os-window-tag <NAME>[¶](#cmdoption-kitty-kitten-panel-name "Link to this definition")
:   On X11 sets the name part of the WM\_CLASS property on X11, when unspecified uses the value from [`kitty --class`](../../invocation/#cmdoption-kitty-app-id) on X11.

--focus-policy <FOCUS\_POLICY>[¶](#cmdoption-kitty-kitten-panel-focus-policy "Link to this definition")
:   On a Wayland compositor that supports the wlr layer shell protocol, specify the focus policy for keyboard interactivity with the panel. Please refer to the wlr layer shell protocol documentation for more details. Note that different Wayland compositors behave very differently with `exclusive`, your mileage may vary. On macOS, `exclusive` and `on-demand` are currently the same.
    Default: `not-allowed`
    Choices: `exclusive`, `not-allowed`, `on-demand`

--hide-on-focus-loss [=no][¶](#cmdoption-kitty-kitten-panel-hide-on-focus-loss "Link to this definition")
:   Automatically hide the panel window when it loses focus. Using this option will force [`--focus-policy`](#cmdoption-kitty-kitten-panel-focus-policy) to `on-demand`. Note that on Wayland, depending on the compositor, this can result in the window never becoming visible.

--grab-keyboard [=no][¶](#cmdoption-kitty-kitten-panel-grab-keyboard "Link to this definition")
:   Grab the keyboard. This means global shortcuts defined in the OS will be passed to kitty instead. Useful if you want to create an OS modal window. How well this works depends on the OS/window manager/desktop environment. On Wayland it works only if the compositor implements the [inhibit-keyboard-shortcuts protocol](https://wayland.app/protocols/keyboard-shortcuts-inhibit-unstable-v1). On macOS Apple doesn’t allow applications to grab the keyboard without special permissions, so it doesn’t work.

--exclusive-zone <EXCLUSIVE\_ZONE>[¶](#cmdoption-kitty-kitten-panel-exclusive-zone "Link to this definition")
:   On a Wayland compositor that supports the wlr layer shell protocol, request a given exclusive zone for the panel. Please refer to the wlr layer shell documentation for more details on the meaning of exclusive and its value. If [`--edge`](#cmdoption-kitty-kitten-panel-edge) is set to anything other than `center` or `none`, this flag will not have any effect unless the flag [`--override-exclusive-zone`](#cmdoption-kitty-kitten-panel-override-exclusive-zone) is also set. If [`--edge`](#cmdoption-kitty-kitten-panel-edge) is set to `background`, this option has no effect. Ignored on X11 and macOS.
    Default: `-1`

--override-exclusive-zone [=no][¶](#cmdoption-kitty-kitten-panel-override-exclusive-zone "Link to this definition")
:   On a Wayland compositor that supports the wlr layer shell protocol, override the default exclusive zone. This has effect only if [`--edge`](#cmdoption-kitty-kitten-panel-edge) is set to `top`, `left`, `bottom` or `right`. Ignored on X11 and macOS.
    Default: `no`

--single-instance [=no], -1 [=no][¶](#cmdoption-kitty-kitten-panel-single-instance "Link to this definition")
:   If specified only a single instance of the panel will run. New invocations will instead create a new top-level window in the existing panel instance.
    Default: `no`

--instance-group <INSTANCE\_GROUP>[¶](#cmdoption-kitty-kitten-panel-instance-group "Link to this definition")
:   default= Used in combination with the [`--single-instance`](#cmdoption-kitty-kitten-panel-single-instance) option. All panel invocations with the same [`--instance-group`](#cmdoption-kitty-kitten-panel-instance-group) will result in new panels being created in the first panel instance within that group.

--wait-for-single-instance-window-close [=no][¶](#cmdoption-kitty-kitten-panel-wait-for-single-instance-window-close "Link to this definition")
:   Normally, when using [`kitty --single-instance`](../../invocation/#cmdoption-kitty-single-instance), kitty will open a new window in an existing instance and quit immediately. With this option, it will not quit till the newly opened window is closed. Note that if no previous instance is found, then kitty will wait anyway, regardless of this option.

--listen-on <LISTEN\_ON>[¶](#cmdoption-kitty-kitten-panel-listen-on "Link to this definition")
:   Listen on the specified socket address for control messages. For example, [`kitty --listen-on`](../../invocation/#cmdoption-kitty-listen-on)`=unix:/tmp/mykitty` or [`kitty --listen-on`](../../invocation/#cmdoption-kitty-listen-on)`=tcp:localhost:12345`. On Linux systems, you can also use abstract UNIX sockets, not associated with a file, like this: [`kitty --listen-on`](../../invocation/#cmdoption-kitty-listen-on)`=unix:@mykitty`. Environment variables are expanded and relative paths are resolved with respect to the temporary directory. To control kitty, you can send commands to it with kitten @ using the [`kitten @ --to`](../../remote-control/#cmdoption-kitten-to) option to specify this address. Note that if you run kitten @ within a kitty window, there is no need to specify the [`kitten @ --to`](../../remote-control/#cmdoption-kitten-to) option as it will automatically read from the environment. Note that this will be ignored unless [`allow_remote_control`](../../conf/#opt-kitty.allow_remote_control) is set to either: `yes`, `socket` or `socket-only`. This can also be specified in `kitty.conf`.

--toggle-visibility [=no][¶](#cmdoption-kitty-kitten-panel-toggle-visibility "Link to this definition")
:   When set and using [`--single-instance`](#cmdoption-kitty-kitten-panel-single-instance) will toggle the visibility of the existing panel rather than creating a new one.
    Default: `no`

--move-to-active-monitor [=no][¶](#cmdoption-kitty-kitten-panel-move-to-active-monitor "Link to this definition")
:   When set and using [`--toggle-visibility`](#cmdoption-kitty-kitten-panel-toggle-visibility) to show an existing panel, the panel is moved to the active monitor (typically the monitor with the mouse on it). This works only if the underlying OS supports it. It is currently supported on macOS only.
    Default: `false`

--start-as-hidden [=no][¶](#cmdoption-kitty-kitten-panel-start-as-hidden "Link to this definition")
:   Start in hidden mode, useful with [`--toggle-visibility`](#cmdoption-kitty-kitten-panel-toggle-visibility).
    Default: `no`

--detach [=no][¶](#cmdoption-kitty-kitten-panel-detach "Link to this definition")
:   Detach from the controlling terminal, if any, running in an independent child process, the parent process exits immediately.
    Default: `no`

--detached-log <DETACHED\_LOG>[¶](#cmdoption-kitty-kitten-panel-detached-log "Link to this definition")
:   default= Path to a log file to store STDOUT/STDERR when using [`--detach`](#cmdoption-kitty-kitten-panel-detach)

--debug-rendering [=no][¶](#cmdoption-kitty-kitten-panel-debug-rendering "Link to this definition")
:   For internal debugging use.

--debug-input [=no][¶](#cmdoption-kitty-kitten-panel-debug-input "Link to this definition")
:   For internal debugging use.

## How the screenshots were generated[¶](#how-the-screenshots-were-generated "Link to this heading")

The system statistics in the background were created using:

```
kitten panel --edge=background -o background_opacity=0.2 -o background=black btop
```

This creates a kitty background window and inside it runs the [btop](https://github.com/aristocratos/btop) program to display the statistics.

The floating quick access window was created by running:

```
kitten quick-access-terminal kitten run-shell \
   zsh -c 'printf "\e]66;s=4;Quick access kitty in Hyprland\a\n\n\n\nAlso uses kitty to draw desktop background\n"'
```

This starts the quick access window and inside it runs `kitten run-shell`, which
in turn first runs `zsh` to print out the message and then starts the users login
shell.

The Linux dock panel was:

```
wm bar
```

This is a custom program I wrote for my personal use. It uses kitty’s kitten
infrastructure to implement the bar in a [few hundred lines of code](https://github.com/kovidgoyal/wm/blob/master/bar/main.go).
This was designed for my personal use only, but, there are [public projects implementing
general purpose panels using kitty](#panel-projects).

## Compatibility with various platforms[¶](#compatibility-with-various-platforms "Link to this heading")

Generated with the help of the `panels.py` test script.

Wayland

Below is a list of the status of various Wayland compositors. The panel kitten
relies of the [wlr layer shell protocol](https://wayland.app/protocols/wlr-layer-shell-unstable-v1#compositor-support),
which is technically supported by almost all Wayland compositors, but the
implementation in some of them is quite buggy.

🟢 **Hyprland**
:   Fully working, no known issues

🟢 **labwc**
:   Fully working, no known issues

🟢 **niri**
:   Fully working, no known issues

🟢 **Xfce**
:   Fully working, no known issues

🟠 **KDE** (kwin)
:   Mostly working, except that clicks outside background panels cause kwin to [erroneously hide the panel](https://github.com/kovidgoyal/kitty/issues/8715). KDE uses an [undocumented mapping](https://invent.kde.org/plasma/kwin/-/blob/3dc5cee6b34792486b343098e55e7f2b90dfcd00/src/layershellv1window.cpp#L24) under Wayland to set the window type from the `kitten panel --app-id` flag. You might want to use `--app-id=dock` so that KDE treats the window as a dock panel, and disables window appearing/disappearing animations for it.

🟠 **Sway**
:   Renders its configured background over the background window instead of
    under it. This is because it uses the wlr protocol for backgrounds itself.

🟠 **river**
:   Breaks when hiding (unmapping) layer shell windows. This means the quick
    access terminal is non-functional, but background and dock panels work.
    More technically, when unmapping the surface (attaching a NULL buffer to
    it) river continues to send configure events to the unmapped surface,
    leading to Wayland protocol errors.

🔴 **GNOME** (mutter)
:   Does not implement the wlr protocol at all, nothing works.

macOS

Mostly everything works, with the notable exception that dock panels do not
prevent other windows from covering them. This is because Apple does not
provide and way to do this in their APIs.

X11

Support is highly dependent on the quirks of individual window
managers. See the matrix below:

Compatibility matrix[¶](#id4 "Link to this table")

| WM | Desktop | Dock | Quick | Notes |
| --- | --- | --- | --- | --- |
| KDE | 🟠 | 🟢 | 🟢 | transparency does not work for [`--edge=background`](#cmdoption-kitty-kitten-panel-edge) |
| GNOME | 🟢 | 🟢 | 🟢 |  |
| XFCE | 🟢 | 🟢 | 🟢 |  |
| i3 | 🔴 | 🟠 | 🔴 | only top and bottom dock panels, without transparency |
| xmonad | 🔴 | 🔴 | 🔴 | doesn’t support the needed NET\_WM protocols |
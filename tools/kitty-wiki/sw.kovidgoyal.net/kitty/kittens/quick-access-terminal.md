---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/quick-access-terminal/"
title: "Make a Quake like quick access terminal - kitty"
crawl_date: "2025-11-16T14:48:27.297964Z"
selector: "article"
---

# Make a Quake like quick access terminal - kitty

# Make a Quake like quick access terminal[¶](#make-a-quake-like-quick-access-terminal "Link to this heading")

Added in version 0.42.0: See [here for what platforms it works on](../panel/#panel-compat).

This kitten can be used to make a quick access terminal, that appears and
disappears at a key press. To do so use the following command:

```
kitten quick-access-terminal
```

Run this command in a terminal, and a quick access kitty window will show up at
the top of your screen. Run it again, and the window will be hidden.

To make the terminal appear and disappear at a key press:

Linux

Simply bind the above command to some key press in your window manager or desktop
environment settings and then you have a quick access terminal at a single key press.

macOS

In kitty, run the above command to show the quick access window, then close
it by running the command again or pressing `ctrl`+`d`. Now go to System Preferences->Keyboard->Keyboard Shortcuts->Services->General and set a shortcut for
the Quick access to kitty entry.

## Configuration[¶](#configuration "Link to this heading")

You can configure the appearance and behavior of the quick access window
by creating a `quick-access-terminal.conf` file in your
[kitty config folder](../../conf/#confloc). In particular, you can use the
[`kitty_conf`](#opt-kitten-quick_access_terminal.kitty_conf) option to change
various kitty settings, just for the quick access window.

Note

This kitten uses the [panel kitten](../panel/) under the
hood. You can use the [techniques described there](../panel/#remote-control-panel)
for remote controlling the quick access window, remember to add
`kitty_override allow_remote_control=socket-only` and `kitty_override
listen_on=unix:/tmp/whatever` to
`quick-access-terminal.conf`.

See below for the supported configuration directives:

## Window appearance[¶](#window-appearance "Link to this heading")

lines[¶](#opt-kitten-quick_access_terminal.lines "Link to this definition")

```
lines 25
```

The number of lines shown in the panel. Ignored for background, centered, and vertical panels. If it has the suffix `px` then it sets the height of the panel in pixels instead of lines.

columns[¶](#opt-kitten-quick_access_terminal.columns "Link to this definition")

```
columns 80
```

The number of columns shown in the panel. Ignored for background, centered, and horizontal panels. If it has the suffix `px` then it sets the width of the panel in pixels instead of columns.

edge[¶](#opt-kitten-quick_access_terminal.edge "Link to this definition")

```
edge top
```

Which edge of the screen to place the panel on. Note that some window managers (such as i3) do not support placing docked windows on the left and right edges. The value `background` means make the panel the “desktop wallpaper”. Note that when using sway if you set a background in your sway config it will cover the background drawn using this kitten. Additionally, there are three more values: `center`, `center-sized` and `none`. The value `center` anchors the panel to all sides and covers the entire display (on macOS the part of the display not covered by titlebar and dock). The panel can be shrunk and placed using the margin parameters. The value `none` anchors the panel to the top left corner and should be placed using the margin parameters. Its size is set by [`lines`](#opt-kitten-quick_access_terminal.lines) and [`columns`](#opt-kitten-quick_access_terminal.columns). The value `center-sized` is just like `none` except that the panel is centered instead of in the top left corner and the margins have no effect.

background\_opacity[¶](#opt-kitten-quick_access_terminal.background_opacity "Link to this definition")

```
background_opacity 0.85
```

The background opacity of the window. This works the same as the kitty
option of the same name, it is present here as it has a different
default value for the quick access terminal.

hide\_on\_focus\_loss[¶](#opt-kitten-quick_access_terminal.hide_on_focus_loss "Link to this definition")

```
hide_on_focus_loss no
```

Hide the window when it loses keyboard focus automatically. Using this option
will force [`focus_policy`](#opt-kitten-quick_access_terminal.focus_policy) to `on-demand`.

grab\_keyboard[¶](#opt-kitten-quick_access_terminal.grab_keyboard "Link to this definition")

```
grab_keyboard no
```

Grab the keyboard. This means global shortcuts defined in the OS will be passed to kitty instead. Useful if
you want to create an OS modal window. How well this
works depends on the OS/window manager/desktop environment. On Wayland it works only if the compositor implements
the [inhibit-keyboard-shortcuts protocol](https://wayland.app/protocols/keyboard-shortcuts-inhibit-unstable-v1).
On macOS Apple doesn’t allow applications to grab the keyboard without special permissions, so it doesn’t work.

margin\_left[¶](#opt-kitten-quick_access_terminal.margin_left "Link to this definition")

```
margin_left 0
```

Set the left margin for the panel, in pixels. Has no effect for right edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.

margin\_right[¶](#opt-kitten-quick_access_terminal.margin_right "Link to this definition")

```
margin_right 0
```

Set the right margin for the panel, in pixels. Has no effect for left edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.

margin\_top[¶](#opt-kitten-quick_access_terminal.margin_top "Link to this definition")

```
margin_top 0
```

Set the top margin for the panel, in pixels. Has no effect for bottom edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.

margin\_bottom[¶](#opt-kitten-quick_access_terminal.margin_bottom "Link to this definition")

```
margin_bottom 0
```

Set the bottom margin for the panel, in pixels. Has no effect for top edge panels. Only works on macOS and Wayland compositors that supports the wlr layer shell protocol.

kitty\_conf[¶](#opt-kitten-quick_access_terminal.kitty_conf "Link to this definition")

Path to config file to use for kitty when drawing the window. Can be specified multiple times. By default, the normal kitty.conf is used. Relative paths are resolved with respect to the kitty config directory.

kitty\_override[¶](#opt-kitten-quick_access_terminal.kitty_override "Link to this definition")

Override individual kitty configuration options, can be specified multiple times. Syntax: kitty\_override name=value. For example: `kitty_override font_size=20`.

app\_id[¶](#opt-kitten-quick_access_terminal.app_id "Link to this definition")

```
app_id kitty-quick-access
```

On Wayland set the namespace of the layer shell surface. On X11 set the WM\_CLASS assigned to the quick access window. (Linux only)

output\_name[¶](#opt-kitten-quick_access_terminal.output_name "Link to this definition")

The panel can only be displayed on a single monitor (output) at a time. This allows you to specify which output is used, by name. If not specified the compositor will choose an output automatically, typically the last output the user interacted with or the primary monitor. Run `kitten panel --output-name list` to get a list of available outputs. Use `listjson` for a json encoded output. Note that on Wayland the output can only be set at panel creation time, it cannot be changed after creation, nor is there anyway to display a single panel on all outputs. Please complain to the Wayland developers about this.

start\_as\_hidden[¶](#opt-kitten-quick_access_terminal.start_as_hidden "Link to this definition")

```
start_as_hidden no
```

Whether to start the quick access terminal hidden. Useful if you are starting it as part of system startup.

focus\_policy[¶](#opt-kitten-quick_access_terminal.focus_policy "Link to this definition")

```
focus_policy exclusive
```

On a Wayland compositor that supports the wlr layer shell protocol, specify the focus policy for keyboard interactivity with the panel. Please refer to the wlr layer shell protocol documentation for more details. Note that different Wayland compositors behave very differently with `exclusive`, your mileage may vary. On macOS, `exclusive` and `on-demand` are currently the same.

## Source code for quick\_access\_terminal[¶](#source-code-for-quick-access-terminal "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/quick_access_terminal).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten quick_access_terminal [options] [cmdline-to-run ...]
```

A quick access terminal window that you can bring up instantly with a keypress or a command.

### Options[¶](#options "Link to this heading")

--config <CONFIG>, -c <CONFIG>[¶](#cmdoption-kitty-kitten-quick_access_terminal-config "Link to this definition")
:   Specify a path to the configuration file(s) to use. All configuration files are merged onto the builtin `quick-access-terminal.conf`, overriding the builtin values. This option can be specified multiple times to read multiple configuration files in sequence, which are merged. Use the special value `NONE` to not load any config file.

    If this option is not specified, config files are searched for in the order: `$XDG_CONFIG_HOME/kitty/quick-access-terminal.conf`, `~/.config/kitty/quick-access-terminal.conf`, `$XDG_CONFIG_DIRS/kitty/quick-access-terminal.conf`. The first one that exists is used as the config file.

    If the environment variable [`KITTY_CONFIG_DIRECTORY`](../../glossary/#envvar-KITTY_CONFIG_DIRECTORY) is specified, that directory is always used and the above searching does not happen.

    If `/etc/xdg/kitty/quick-access-terminal.conf` exists, it is merged before (i.e. with lower priority) than any user config files. It can be used to specify system-wide defaults for all users. You can use either `-` or `/dev/stdin` to read the config from STDIN.

--override <OVERRIDE>, -o <OVERRIDE>[¶](#cmdoption-kitty-kitten-quick_access_terminal-override "Link to this definition")
:   Override individual configuration options, can be specified multiple times. Syntax: name=value. For example: -o lines=12

--detach [=no][¶](#cmdoption-kitty-kitten-quick_access_terminal-detach "Link to this definition")
:   Detach from the controlling terminal, if any, running in an independent child process, the parent process exits immediately.

--detached-log <DETACHED\_LOG>[¶](#cmdoption-kitty-kitten-quick_access_terminal-detached-log "Link to this definition")
:   Path to a log file to store STDOUT/STDERR when using [`--detach`](#cmdoption-kitty-kitten-quick_access_terminal-detach)

--instance-group <INSTANCE\_GROUP>[¶](#cmdoption-kitty-kitten-quick_access_terminal-instance-group "Link to this definition")
:   The unique name of this quick access terminal Use a different name if you want multiple such terminals.
    Default: `quick-access`

--debug-rendering [=no][¶](#cmdoption-kitty-kitten-quick_access_terminal-debug-rendering "Link to this definition")
:   For debugging interactions with the compositor/window manager.

--debug-input [=no][¶](#cmdoption-kitty-kitten-quick_access_terminal-debug-input "Link to this definition")
:   For debugging interactions with the compositor/window manager.

## Sample quick-access-terminal.conf[¶](#sample-quick-access-terminal-conf "Link to this heading")

You can download a sample `quick-access-terminal.conf` file with all default settings and
comments describing each setting by clicking: [`sample quick-access-terminal.conf`](../../_downloads/055e3591463099e42785a872ce39996a/quick_access_terminal.conf).
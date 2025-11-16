---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/desktop-ui/"
title: "Using terminal programs to provide Linux desktop components - kitty"
crawl_date: "2025-11-16T14:48:51.632794Z"
selector: "article"
---

# Using terminal programs to provide Linux desktop components - kitty

# Using terminal programs to provide Linux desktop components[¶](#using-terminal-programs-to-provide-linux-desktop-components "Link to this heading")

Added in version 0.43.0.

Power users of terminals on Linux also often like to use bare bones window
managers instead of full fledged desktop environments. This kitten helps
provide parts of the desktop environment that are missing from such setups,
and does so using keyboard friendly, terminal first UI components. Some of its
features are:

* Replace the typical File Open/Save dialogs used in GUI programs with the
  fast and keyboard centric [choose-files](../choose-files/) kitten
  running in a semi-transparent kitty overlay.
* Allow simple command line based management of the desktop light/dark modes.

## How to install[¶](#how-to-install "Link to this heading")

Note

This kitten relies on the [panel kitten](../panel/)
under the hood to supply UI components. Check [the documentation](../panel/#panel-compat)
of that kitten to see if your window manager works with it.

First, run:

```
kitten desktop-ui enable-portal
```

Then, set the following two environment variables, *system wide*, that means in
`/etc/environment` or the equivalent for your distribution:

```
QT_QPA_PLATFORMTHEME=xdgdesktopportal
GTK_USE_PORTAL=1
```

Finally, reboot. Now, when you open a file dialog in most GUI applications, it
should open the [choose-files kitten](../choose-files/) instead
of a normal file open dialog. You can change the current light/dark mode of
your desktop by running:

```
kitten desktop-ui set-color-scheme dark
kitten desktop-ui set-color-scheme light
```

Check the current value using:

```
dbus-send --session --print-reply --dest=org.freedesktop.portal.Desktop /org/freedesktop/portal/desktop org.freedesktop.portal.Settings.Read string:org.freedesktop.appearance string:color-scheme
```

## How it works[¶](#how-it-works "Link to this heading")

Modern Linux desktops have so called [portals](https://flatpak.github.io/xdg-desktop-portal/docs/index.html) that were
invented for sandboxed applications and provide various facilities to such
applications over DBUS, including file open dialogs, common desktop settings,
etc. This kitten works by implementing a backend for some of these services.

Normal GUI applications can then be told to make use of these services, thereby
allowing us to replace parts of the desktop experience as needed.

There are multiple competing implementations of the backends. Each desktop
environment like KDE or GNOME has it’s own backend and many window managers
provide implementations for some backends as well. Service discovery and
configuring which backend to use happens via the `xdg-desktop-portal`
program, usually found at `/usr/lib/xdg-desktop-portal`.

It can be configured by files in `~/.local/share/xdg-desktop-portal`. See
[man portals.conf](https://man.archlinux.org/man/portals.conf.5). The
`kitten desktop-ui enable-portal` command takes care of the setup for you
automatically. If you want to customize exactly which services to use this
kitten for, run the command and then edit the conf file that the command says
it has patched.

## Troubleshooting[¶](#troubleshooting "Link to this heading")

First, ensure that DBUS is able to auto-start the kitten when it is needed. If
the kitten is not already running, try the following command:

```
dbus-send --session --print-reply --dest=org.freedesktop.impl.portal.desktop.kitty \
    /net/kovidgoyal/kitty/portal org.freedesktop.DBus.Properties.GetAll \
    string:net.kovidgoyal.kitty.settings
```

If DBUS is able to start the kitten or if it is already running it will print
out the version property, otherwise it will fail with an error. If it fails,
check the file
`~/.local/share/dbus-1/services/org.freedesktop.impl.portal.desktop.kitty.service`
that should have been created by the `enable-portal` command. It’s `Exec`
key must point to the full path to the kitten executable.

Next, check that the XDG portal system is actually using this kitten for its
settings backend. Run:

```
dbus-send --session --print-reply --dest=org.freedesktop.portal.Desktop \
    /org/freedesktop/portal/desktop org.freedesktop.portal.Settings.Read \
    string:net.kovidgoyal.kitty string:status
```

If this returns a reply then the kitten is being used, as expected. If it
returns a not found error, then some other backend is being used for settings.

Read the `portals.conf` man page and run:

```
/usr/lib/xdg-desktop-portal -r v
```

this will output a lot of debug information, which should tell you which
backend is chosen for which service. Read the debug output carefully to
determine why the kitten is not being selected.

If some GUI applications are not using the choose-files kitten for their file
select dialogs, then make sure the environment variables mentioned above are
set, you can also try running the the GUI application with them set explicitly,
as:

```
QT_QPA_PLATFORMTHEME=xdgdesktopportal GTK_USE_PORTAL=1 my-gui-app
```

Note that not all applications use portals, so if some particular application
is failing to use the portal but others work, report the issue to that
applications’ developers.
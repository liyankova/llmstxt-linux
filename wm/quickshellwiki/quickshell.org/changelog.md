---
source_url: "https://quickshell.org/changelog"
title: "Changelog"
crawl_date: "2025-11-16T14:36:13.896574Z"
selector: ".docslayout"
---

# Changelog

### [Quickshell](/)

`CtrlK`   

Cancel

  

Changelog

---

- [master](#master)
- [v0.2.1](#v0.2.1)
- [v0.2.0](#v0.2.0)
- [v0.1.0](#v0.1.0)

2. [Changelog](/changelog)
 

---

# Changelog

## master

## [Documentation](/docs/master/guide)

---

## Breaking Changes

### Config paths are no longer canonicalized

This fixes nix configs changing shell-ids on rebuild as the shell id is now derived from
the symlink path. Configs with a symlink in their path will have a different shell id.

Shell ids are used to derive the default config / state / cache folders, so those files
will need to be manually moved if using a config behind a symlinked path without an explicitly
set shell id.

## New Features

* Added support for creating Polkit agents.
* Added support for creating wayland idle inhibitors.
* Added support for wayland idle timeouts.
* Added the ability to override Quickshell.cacheDir with a custom path.

## Other Changes

* IPC operations filter available instances to the current display connection by default.

## Bug Fixes

* Fixed volume control breaking with pipewire pro audio mode.
* Fixed escape sequence handling in desktop entries.

## Packaging Changes

`glib` and `polkit` have been added as dependencies when compiling with polkit agent support.

## v0.2.1

## [Documentation](/docs/v0.2.1/guide)

---

## New Features

* Changes to desktop entries are now tracked in real time.

## Other Changes

* Added support for Qt 6.10

## Bug Fixes

* Fixed volumes getting stuck on change for pipewire devices with few volume steps.
* Fixed a crash when running out of disk space to write log files.
* Fixed a rare crash when disconnecting a monitor.
* Fixed build issues preventing cross compilation from working.
* Fixed dekstop entries with lower priority than a hidden entry not being hidden.
* Fixed desktop entry keys with mismatched modifier or country not being discarded.
* Fixed greetd hanging when authenticating with a fingerprint.

## v0.2.0

## [Documentation](/docs/v0.2.0/guide)

---

## Breaking Changes

* Files outside of the shell directory can no longer be referenced with relative paths, e.g. ’../../foo.png’.
* PanelWindow’s Automatic exclusion mode now adds an exclusion zone for panels with a single anchor.
* `QT_QUICK_CONTROLS_STYLE` and `QT_STYLE_OVERRIDE` are ignored unless `//@ pragma RespectSystemStyle` is set.

## New Features

### Root-Relative Imports

Quickshell 0.2 comes with a new method to import QML modules which is supported by QMLLS.
This replaces “root:/” imports for QML modules.

The new syntax is `import qs.path.to.module`, where `path/to/module` is the path to
a module/subdirectory relative to the config root (`qs`).

### Better LSP support

LSP support for Singletons and Root-Relative imports can be enabled by creating a file named
`.qmlls.ini` in the shell root directory. Quickshell will detect this file and automatically
populate it with an LSP configuration. This file should be gitignored in your configuration,
as it is system dependent.

The generated configuration also includes QML import paths available to Quickshell, meaning
QMLLS no longer requires the `-E` flag.

### Bluetooth Module

Quickshell can now manage your bluetooth devices through BlueZ. While authenticated pairing
has not landed in 0.2, support for connecting and disconnecting devices, basic device information,
and non-authenticated pairing are now supported.

### Other Features

* Added `HyprlandToplevel` and related toplevel/window management APIs in the Hyprland module.
* Added `Quickshell.execDetached()`, which spawns a detached process without a `Process` object.
* Added `Process.exec()` for easier reconfiguration of process commands when starting them.
* Added `FloatingWindow.title`, which allows changing the title of a floating window.
* Added `signal QsWindow.closed()`, fired when a window is closed externally.
* Added support for inline replies in notifications, when supported by applications.
* Added `DesktopEntry.startupWmClass` and `DesktopEntry.heuristicLookup()` to better identify toplevels.
* Added `DesktopEntry.command` which can be run as an alternative to `DesktopEntry.execute()`.
* Added `//@ pragma Internal`, which makes a QML component impossible to import outside of its module.
* Added dead instance selection for some subcommands, such as `qs log` and `qs list`.

## Other Changes

* `Quickshell.shellRoot` has been renamed to `Quickshell.shellDir`.
* PanelWindow margins opposite the window’s anchorpoint are now added to exclusion zone.
* stdout/stderr or detached processes and executed desktop entries are now hidden by default.
* Various warnings caused by other applications Quickshell communicates with over D-BUS have been hidden in logs.
* Quickshell’s new logo is now shown in any floating windows.

## Bug Fixes

* Fixed pipewire device volume and mute states not updating before the device has been used.
* Fixed a crash when changing the volume of any pipewire device on a sound card another removed device was using.
* Fixed a crash when accessing a removed previous default pipewire node from the default sink/source changed signals.
* Fixed session locks crashing if all monitors are disconnected.
* Fixed session locks crashing if unsupported by the compositor.
* Fixed a crash when creating a session lock and destroying it before acknowledged by the compositor.
* Fixed window input masks not updating after a reload.
* Fixed PanelWindows being unconfigurable unless `screen` was set under X11.
* Fixed a crash when anchoring a popup to a zero sized `Item`.
* Fixed `FileView` crashing if `watchChanges` was used.
* Fixed `SocketServer` sockets disappearing after a reload.
* Fixed `ScreencopyView` having incorrect rotation when displaying a rotated monitor.
* Fixed `MarginWrapperManager` breaking pixel alignment of child items when centering.
* Fixed `IpcHandler`, `NotificationServer` and `GlobalShortcut` not activating with certain QML structures.
* Fixed tracking of QML incubator destruction and deregistration, which occasionally caused crashes.
* Fixed FloatingWindows being constrained to the smallest window manager supported size unless max size was set.
* Fixed `MprisPlayer.lengthSupported` not updating reactively.
* Fixed normal tray icon being ignored when status is `NeedsAttention` and no attention icon is provided.
* Fixed `HyprlandWorkspace.activate()` sending invalid commands to Hyprland for named or special workspaces.
* Fixed file watcher occasionally breaking when using VSCode to edit QML files.
* Fixed crashes when screencopy buffer creation fails.
* Fixed a crash when wayland layer surfaces are recreated for the same window.
* Fixed the `QsWindow` attached object not working when using `WlrLayershell` directly.
* Fixed a crash when attempting to create a window without available VRAM.
* Fixed OOM crash when failing to write to detailed log file.
* Prevented distro logging configurations for Qt from interfering with Quickshell commands.
* Removed the “QProcess destroyed for running process” warning when destroying `Process` objects.
* Fixed `ColorQuantizer` printing a pointer to an error message instead of an error message.
* Fixed notification pixmap rowstride warning showing for correct rowstrides.

## v0.1.0

## [Documentation](/docs/v0.1.0/guide)

---

Initial release

Changelog

---

- [master](#master)
- [v0.2.1](#v0.2.1)
- [v0.2.0](#v0.2.0)
- [v0.1.0](#v0.1.0)
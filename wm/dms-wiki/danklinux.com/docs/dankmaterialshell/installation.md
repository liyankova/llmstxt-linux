---
source_url: "https://danklinux.com/docs/dankmaterialshell/installation"
title: "Installation | Dank Linux"
crawl_date: "2025-11-16T08:41:55.196360Z"
selector: "article"
---

# Installation | Dank Linux

* DankMaterialShell (dms)
* Installation

On this page

```
██████╗ ███╗   ███╗███████╗
██╔══██╗████╗ ████║██╔════╝
██║  ██║██╔████╔██║███████╗
██║  ██║██║╚██╔╝██║╚════██║
██████╔╝██║ ╚═╝ ██║███████║
╚═════╝ ╚═╝     ╚═╝╚══════╝
```

This guide covers installation of DankMaterialShell across different Linux distributions and methods.

## Dependencies[​](#dependencies "Direct link to Dependencies")

note

Only **Quickshell** is required. All other dependencies are optional and enable specific features.

* **Quickshell** (required) - The core framework
* **dgop** (optional) - System telemetry for resource widgets
* **dsearch** (optional) - Filesystem search engine
* **matugen** (optional) - Material Design color palette generation
* **wl-clipboard** + **cliphist** (optional) - Clipboard history
* **cava** (optional) - Audio visualizer widget
* **qt6-multimedia** (optional) - System sound feedback

## Arch & Derivatives[​](#arch--derivatives "Direct link to Arch & Derivatives")

`dms` is available on the [AUR](https://aur.archlinux.org/), it is assumed that you have an aur helper installed such as [paru](https://aur.archlinux.org/packages/paru) or [yay](https://aur.archlinux.org/packages/yay).

For the sake of consistency, we will use `paru` in the examples.

### Stable Release[​](#stable-release "Direct link to Stable Release")

```
paru -S dms-shell-bin
```

### Latest Development Build[​](#latest-development-build "Direct link to Latest Development Build")

```
paru -S dms-shell-git
```

These packages ship the shell, widgets, and CLI. Pair them with the `niri`, `hyprland`, `sway`, or `dwl` (via MangoWC) packages from the official repositories for a complete desktop stack.

## Fedora & Derivatives[​](#fedora--derivatives "Direct link to Fedora & Derivatives")

Enable the COPR repositories managed by the team to install prebuilt packages:

### Stable Release[​](#stable-release-1 "Direct link to Stable Release")

```
sudo dnf copr enable avengemedia/dms  
sudo dnf install dms
```

### Latest Development Build[​](#latest-development-build-1 "Direct link to Latest Development Build")

```
sudo dnf copr enable avengemedia/dms-git  
sudo dnf install dms
```

The COPR repositories also provide companion packages such as `quickshell-git`, `cliphist`, `ghostty`, and other utilities used by the default configuration.

## NixOS[​](#nixos "Direct link to NixOS")

tip

NixOS has dedicated documentation. See the [NixOS installation guide](/docs/dankmaterialshell/nixos) for flake-based setup.

## All Other Distributions[​](#all-other-distributions "Direct link to All Other Distributions")

warning

This guide doesn't cover compositor installation. You need a compatible Wayland compositor (niri, Hyprland, sway, dwl/MangoWC, etc.).

### 1. Install Essential Dependencies[​](#1-install-essential-dependencies "Direct link to 1. Install Essential Dependencies")

#### Quickshell[​](#quickshell "Direct link to Quickshell")

If your distribution does not provide a quickshell package, you'll need to build it from source. Quickshell requires:

**Base dependencies:**

* cmake, qt6base, qt6declarative, qtshadertools, pkg-config, cli11
* Private Qt headers for qt6declarative (and qt6wayland on Qt < 6.10)
* Qt 6.6 or newer

**Key features and their dependencies:**

* **Wayland support** (enabled by default) - qt6wayland, wayland, wayland-protocols
* **Crash reporter** (recommended) - google-breakpad
* **Jemalloc** (recommended for better memory management) - jemalloc
* **System tray** - qt6dbus
* **PAM authentication** - pam

For complete build instructions and feature flags, see the [Quickshell BUILD.md](https://git.outfoxxed.me/quickshell/quickshell/raw/branch/master/BUILD.md).

#### AccountsService[​](#accountsservice "Direct link to AccountsService")

note

AccountsService is needed to persist user profile configurations such as profile pictures. Available in most repositories as `accountsservice`.

```
# Arch + Friends  
sudo pacman -S accountsservice  
# Fedora + Friends  
sudo dnf install accountsservice  
# Debian, Ubuntu + Friends  
sudo apt install accountsservice  
# openSUSE + Friends  
sudo zypper install accountsservice  
# Gentoo  
sudo emerge --ask sys-apps/accountsservice
```

### 2. Clone the DMS Repository[​](#2-clone-the-dms-repository "Direct link to 2. Clone the DMS Repository")

```
mkdir -p ~/.config/quickshell  
git clone https://github.com/AvengeMedia/DankMaterialShell.git ~/.config/quickshell/dms
```

### 3. Compile & Install the DMS Backend[​](#3-compile--install-the-dms-backend "Direct link to 3. Compile & Install the DMS Backend")

*Requires GO 1.24+*

```
cd ~/.config/quickshell/dms/backend  
make && sudo make install
```

### 4. Install Optional Integrations[​](#4-install-optional-integrations "Direct link to 4. Install Optional Integrations")

Install optional components for full functionality using your distribution's package manager:

* `dgop` - Detailed system metrics and process lists
* `dsearch` - Filesystem search engine
* `matugen` - Material Design color palette generation
* `i2c-tools` - ddc monitor backlight control
* `wl-clipboard` + `cliphist` - Clipboard history
* `cava` - Audio visualizer widget
* `qt6-multimedia` - System sound feedback

## Post Install[​](#post-install "Direct link to Post Install")

After completing installation:

1. Launch the shell with `dms run`
2. Use `dms restart` or `dms kill` to manage the session during upgrades
3. Configure your compositor - see the [Keybinds & IPC](/docs/dankmaterialshell/keybinds-ipc) guide
4. Customize appearance via [Themes](/docs/dankmaterialshell/application-themes)
5. Extend functionality with [Plugins](/docs/dankmaterialshell/plugins-overview)

### Systemd Integration[​](#systemd-integration "Direct link to Systemd Integration")

Available on Arch, Fedora, and Source Builds

DMS now supports native systemd management for automatic startup and lifecycle control.

**Enable autostart:**

```
systemctl --user enable dms.service
```

**Manual control:**

```
# Start DMS now  
systemctl --user start dms.service  
  
# Check status  
systemctl --user status dms.service  
  
# View logs  
journalctl --user -u dms.service -f  
  
# Restart DMS  
systemctl --user restart dms.service  
  
# Disable autostart  
systemctl --user disable dms.service
```

warning

If using systemd autostart, remove `dms run` / `spawn "dms" "run"` from your compositor's configuration to avoid running DMS twice.
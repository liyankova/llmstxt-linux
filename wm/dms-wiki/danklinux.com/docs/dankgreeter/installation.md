---
source_url: "https://danklinux.com/docs/dankgreeter/installation"
title: "Installation | Dank Linux"
crawl_date: "2025-11-16T08:43:33.718374Z"
selector: "article"
---

# Installation | Dank Linux

* DankGreeter (dms-greeter)
* Installation

On this page

```
██████╗  █████╗ ███╗   ██╗██╗  ██╗ ██████╗ ██████╗ ███████╗███████╗████████╗
██╔══██╗██╔══██╗████╗  ██║██║ ██╔╝██╔════╝ ██╔══██╗██╔════╝██╔════╝╚══██╔══╝
██║  ██║███████║██╔██╗ ██║█████╔╝ ██║  ███╗██████╔╝█████╗  █████╗     ██║
██║  ██║██╔══██║██║╚██╗██║██╔═██╗ ██║   ██║██╔══██╗██╔══╝  ██╔══╝     ██║
██████╔╝██║  ██║██║ ╚████║██║  ██╗╚██████╔╝██║  ██║███████╗███████╗   ██║
╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝╚══════╝   ╚═╝
```

## Installation Methods[​](#installation-methods "Direct link to Installation Methods")

### For dankinstall users[​](#for-dankinstall-users "Direct link to For dankinstall users")

If you installed DMS using [dankinstall](/docs/dankinstall), you can automate the entire installation and setup process:

#### 1. Install and Configure[​](#1-install-and-configure "Direct link to 1. Install and Configure")

```
dms greeter install
```

This command will automatically:

* Install greetd (if not already installed)
* Set up the dms-greeter wrapper
* Configure permissions and ACLs for theme syncing
* Create the greeter cache directory
* Configure greetd to use DMS

warning

**Important:** The `dms greeter install` command should **ONLY** be run if you installed DMS via dankinstall. If you installed DMS via Arch AUR, Fedora COPR, or NixOS, skip this step and use the installation instructions below.

#### 2. Enable the Greeter[​](#2-enable-the-greeter "Direct link to 2. Enable the Greeter")

```
dms greeter enable
```

This will:

* Configure `/etc/greetd/config.toml` with the correct compositor command
* Disable conflicting display managers (gdm, lightdm, sddm)
* Enable and start the greetd service

#### 3. Sync with Your User Theme[​](#3-sync-with-your-user-theme "Direct link to 3. Sync with Your User Theme")

```
dms greeter sync
```

This will:

* Add your user to the `greeter` group (if needed)
* Set up ACL permissions on parent directories for greeter access
* Configure group permissions on DMS config directories
* Create symlinks to sync settings, wallpapers, and color themes

note

After running `dms greeter sync`, you will need to log out and log back in for group membership changes to take effect.

### For Arch AUR and Fedora users[​](#for-arch-aur-and-fedora-users "Direct link to For Arch AUR and Fedora users")

Follow the installation steps below for your distribution, then proceed to [Completing Setup](#completing-setup) to enable and sync the greeter.

## Arch Linux[​](#arch-linux "Direct link to Arch Linux")

Install from the AUR:

```
paru -S greetd-dms-greeter-git  
# Or with yay  
yay -S greetd-dms-greeter-git
```

After installation, proceed to [Completing Setup](#completing-setup) below.

## Fedora[​](#fedora "Direct link to Fedora")

```
sudo dnf copr enable avengemedia/danklinux  
sudo dnf install dms-greeter
```

After installation, proceed to [Completing Setup](#completing-setup) below.

## Other distributions[​](#other-distributions "Direct link to Other distributions")

Install `greetd`, `quickshell`, and then the greeter:

```
sudo mkdir -p /etc/xdg/quickshell  
sudo git clone https://github.com/AvengeMedia/DankMaterialShell.git /etc/xdg/quickshell/dms-greeter  
sudo mkdir /var/cache/dms-greeter  
sudo chown greeter:greeter /var/cache/dms-greeter
```

note

Some distributions may have different user/group names for the greetd user.

#### Prerequisites for Theme Syncing[​](#prerequisites-for-theme-syncing "Direct link to Prerequisites for Theme Syncing")

If you want to sync your user's theme with the greeter, ensure the `acl` package is installed.
ACLs (Access Control Lists) are required to allow the greeter user to traverse your home directory and access configuration files.

## Completing Setup[​](#completing-setup "Direct link to Completing Setup")

After installing the greeter package, you can use automated commands to complete setup, or follow manual steps.

### Automated Setup (Arch and Fedora users)[​](#automated-setup-arch-and-fedora-users "Direct link to Automated Setup (Arch and Fedora users)")

After installing the greeter package, you can use these commands:

#### 1. Enable the Greeter[​](#1-enable-the-greeter "Direct link to 1. Enable the Greeter")

```
dms greeter enable
```

This will:

* Configure `/etc/greetd/config.toml` with the correct compositor command
* Disable conflicting display managers (gdm, lightdm, sddm)
* Enable and start the greetd service

#### 2. Sync with Your User Theme[​](#2-sync-with-your-user-theme "Direct link to 2. Sync with Your User Theme")

```
dms greeter sync
```

This will:

* Add your user to the `greeter` group (if needed)
* Set up ACL permissions on parent directories for greeter access
* Configure group permissions on DMS config directories
* Create symlinks to sync settings, wallpapers, and color themes

note

After running `dms greeter sync`, you will need to log out and log back in for group membership changes to take effect.

note

**NixOS users:** The `dms greeter enable` and `dms greeter sync` commands are not available on NixOS. Please follow the manual steps below or see the [NixOS guide](/docs/dankgreeter/nixos).

### For all users[​](#for-all-users "Direct link to For all users")

You can check your greeter configuration at any time:

```
dms greeter status
```

This verifies your greeter setup and sync status. See the [Configuration guide](/docs/dankgreeter/configuration#checking-sync-status) for detailed information.

---

### Manual Setup (all distros)[​](#manual-setup-all-distros "Direct link to Manual Setup (all distros)")

If you prefer to set up the greeter manually, follow these steps:

tip

**Arch and Fedora users:** You can use `dms greeter enable` to automate this process instead of following the manual steps below.

1. Edit `/etc/greetd/config.toml` and set `command =` to use dms-greeter:

```
[terminal]  
vt = 1  
  
[default_session]  
user = "greeter"  
command = "dms-greeter --command niri"  
### Uncomment the below line to run the greeter on Hyprland  
# command = "dms-greeter --command Hyprland"  
### Uncomment to run the greeter on sway  
# command = "dms-greeter --command sway"
```

2. Disable any existing conflicting greeters:

warning

Disabling a greeter while logged in under that greeter will log you out and bring you to a non-graphical TTY.

```
sudo systemctl disable gdm lightdm sddm
```

3. Enable and start the greeter:

```
sudo systemctl enable greetd  
sudo systemctl start greetd
```
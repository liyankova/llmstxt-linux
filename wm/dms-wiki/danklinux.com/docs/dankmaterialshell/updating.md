---
source_url: "https://danklinux.com/docs/dankmaterialshell/updating"
title: "Updating | Dank Linux"
crawl_date: "2025-11-16T08:42:07.492499Z"
selector: "article"
---

# Updating | Dank Linux

* DankMaterialShell (dms)
* Updating

On this page

```
██████╗ ███╗   ███╗███████╗
██╔══██╗████╗ ████║██╔════╝
██║  ██║██╔████╔██║███████╗
██║  ██║██║╚██╔╝██║╚════██║
██████╔╝██║ ╚═╝ ██║███████║
╚═════╝ ╚═╝     ╚═╝╚══════╝
```

This guide covers how to update DankMaterialShell across different installation methods.

## Package Installations[​](#package-installations "Direct link to Package Installations")

### Arch & Derivatives[​](#arch--derivatives "Direct link to Arch & Derivatives")

For both stable and git versions, use your AUR helper:

```
paru -Syu dms-shell-bin  
# or  
paru -Syu dms-shell-git  
# or, update all installed AUR/devel packages  
paru -Sua
```

After the package updates, restart the shell:

```
dms restart
```

### Fedora & Derivatives[​](#fedora--derivatives "Direct link to Fedora & Derivatives")

Update through DNF as normal:

```
sudo dnf upgrade dms
```

Then restart the shell:

```
dms restart
```

### NixOS[​](#nixos "Direct link to NixOS")

Update your flake inputs or system configuration and rebuild:

```
sudo nixos-rebuild switch
```

## Manual Installations[​](#manual-installations "Direct link to Manual Installations")

For manual installations, you can use the dms CLI to update.

```
dms update
```

For manually compiled packages (some distributions - Debian, Ubuntu, openSUSE). You may need to update quickshell, niri, Hyprland, or other dependencies. You can do that with the interactive tui.

```
dms  
# Navigate to update -> toggle all packages you wish to update/recompile
```

## After Updating[​](#after-updating "Direct link to After Updating")

After any update:

1. Fully restart dms - `dms restart`.
2. Check release notes for breaking changes or new features
3. Review settings if new options are available
4. Update plugins to ensure compatibility

## Troubleshooting Updates[​](#troubleshooting-updates "Direct link to Troubleshooting Updates")

If you experience issues after updating:

1. **Reset settings:** Backup and remove `~/.config/DankMaterialShell/settings.json`, then restart to regenerate defaults
2. **Check logs:** Run `dms kill && dms run` from a terminal to watch logs.
3. **Verify dependencies:** Ensure Quickshell and optional components are up to date
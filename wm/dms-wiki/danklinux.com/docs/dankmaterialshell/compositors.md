---
source_url: "https://danklinux.com/docs/dankmaterialshell/compositors"
title: "Compositor Setup | Dank Linux"
crawl_date: "2025-11-16T08:42:14.443157Z"
selector: "article"
---

# Compositor Setup | Dank Linux

* DankMaterialShell (dms)
* Compositor Setup

On this page

```
██████╗ ███╗   ███╗███████╗
██╔══██╗████╗ ████║██╔════╝
██║  ██║██╔████╔██║███████╗
██║  ██║██║╚██╔╝██║╚════██║
██████╔╝██║ ╚═╝ ██║███████║
╚═════╝ ╚═╝     ╚═╝╚══════╝
```

DankMaterialShell works with any Wayland compositor, but we provide optimized configurations for niri, Hyprland, [Sway](https://swaywm.org/), and dwl/MangoWC. These configs include DMS-specific keybindings, proper layer shell rules, and recommended settings.

## niri Configuration[​](#niri-configuration "Direct link to niri Configuration")

niri uses the KDL configuration format. DankMaterialShell integrates seamlessly with niri's scrollable tiling layout.

warning

niri's configuration is not repeatable. The settings below are snippets you must merge with existing configuration. You cannot have multiple `layout {}` sections.

### Key Configuration Sections[​](#key-configuration-sections "Direct link to Key Configuration Sections")

tip

The next niri release will support automatic gap and color synchronization with DMS. Not available in current stable.

```
// Add to the top of ~/.config/niri.config.kdls  
include "dms/binds.kdl"  
  
// Add to the end of ~/.config/niri/config.kdl  
include "dms/colors.kdl"  
include "dms/layout.kdl"
```

For manual configuration recommendations, continue below.

#### Layout[​](#layout "Direct link to Layout")

The niri layout should have a transparent background, in order to integrate wallpapers onto the overview.

```
layout {  
    // You can tailor the gaps to fit dms spacing.  
    gaps 5  
    background-color "transparent"  
}
```

#### Layer Rules[​](#layer-rules "Direct link to Layer Rules")

Tell niri to place the wallpaper on the overview.

```
layer-rule {  
    match namespace="^quickshell$"  
    place-within-backdrop true  
}
```

If "Blur Layer" is enabled, you can place the blurred wallpaper on the overview.

```
layer-rule {  
    match namespace="dms:blurwallpaper"  
    place-within-backdrop true  
}
```

For more about layer rules see [layer rules](/docs/dankmaterialshell/layers).

#### Startup[​](#startup "Direct link to Startup")

Launch DankMaterialShell and optional services:

```
// Clipboard history  
spawn-at-startup "bash" "-c" "wl-paste --watch cliphist store &"  
// Start the shell  
spawn-at-startup "dms" "run"  
// (Optional) replace with a polkit agent for escalation prompts  
// spawn-at-startup "{{POLKIT_AGENT_PATH}}"
```

#### Environment Variables[​](#environment-variables "Direct link to Environment Variables")

```
environment {  
  XDG_CURRENT_DESKTOP "niri"  
  QT_QPA_PLATFORM "wayland"  
  ELECTRON_OZONE_PLATFORM_HINT "auto"  
  QT_QPA_PLATFORMTHEME "gtk3"  
  QT_QPA_PLATFORMTHEME_QT6 "gtk3"  
}
```

#### DMS Keybindings[​](#dms-keybindings "Direct link to DMS Keybindings")

For the full list of available IPC commands see [IPC](/docs/dankmaterialshell/keybinds-ipc)

```
binds {  
    // Application Launchers  
    Mod+Space hotkey-overlay-title="Application Launcher" {  
        spawn "dms" "ipc" "call" "spotlight" "toggle";  
    }  
    Mod+V hotkey-overlay-title="Clipboard Manager" {  
        spawn "dms" "ipc" "call" "clipboard" "toggle";  
    }  
    Mod+M hotkey-overlay-title="Task Manager" {  
        spawn "dms" "ipc" "call" "processlist" "toggle";  
    }  
    Mod+Comma hotkey-overlay-title="Settings" {  
        spawn "dms" "ipc" "call" "settings" "toggle";  
    }  
    Mod+N hotkey-overlay-title="Notification Center" {  
        spawn "dms" "ipc" "call" "notifications" "toggle";  
    }  
    Mod+Y hotkey-overlay-title="Browse Wallpapers" {  
        spawn "dms" "ipc" "call" "dankdash" "wallpaper";  
    }  
  
    // Security  
    Mod+Alt+L hotkey-overlay-title="Lock Screen" {  
        spawn "dms" "ipc" "call" "lock" "lock";  
    }  
  
    // Audio Controls  
    XF86AudioRaiseVolume allow-when-locked=true {  
        spawn "dms" "ipc" "call" "audio" "increment" "3";  
    }  
    XF86AudioLowerVolume allow-when-locked=true {  
        spawn "dms" "ipc" "call" "audio" "decrement" "3";  
    }  
    XF86AudioMute allow-when-locked=true {  
        spawn "dms" "ipc" "call" "audio" "mute";  
    }  
  
    // Brightness Controls  
    XF86MonBrightnessUp allow-when-locked=true {  
       spawn "dms" "ipc" "call" "brightness" "increment" "5" "";  
    }  
    XF86MonBrightnessDown allow-when-locked=true {  
       spawn "dms" "ipc" "call" "brightness" "decrement" "5" "";  
    }  
}
```

### Window Rules[​](#window-rules "Direct link to Window Rules")

Recommended window rules, tailor to your preferences:

```
window-rule {  
    match app-id=r#"^org\.gnome\."#  
    draw-border-with-background false  
    geometry-corner-radius 12  
    clip-to-geometry true  
}  
  
window-rule {  
    match app-id=r#"^org\.wezfurlong\.wezterm$"#  
    match app-id="Alacritty"  
    match app-id="zen"  
    match app-id="com.mitchellh.ghostty"  
    match app-id="kitty"  
    draw-border-with-background false  
}  
  
window-rule {  
    match is-active=false  
    opacity 0.9  
}  
  
window-rule {  
    geometry-corner-radius 12  
    clip-to-geometry true  
}
```

## Hyprland Configuration[​](#hyprland-configuration "Direct link to Hyprland Configuration")

Hyprland uses a simple config file format at `~/.config/hypr/hyprland.conf`.

### Key Configuration Sections[​](#key-configuration-sections-1 "Direct link to Key Configuration Sections")

#### Startup[​](#startup-1 "Direct link to Startup")

```
exec-once = bash -c "wl-paste --watch cliphist store &"  
exec-once = dms run  
exec-once = {{POLKIT_AGENT_PATH}}
```

#### Miscellaneous[​](#miscellaneous "Direct link to Miscellaneous")

Disables the hyprland backdrop/logo

```
misc {  
    disable_hyprland_logo = true  
    disable_splash_rendering = true  
}
```

#### Environment Variables[​](#environment-variables-1 "Direct link to Environment Variables")

```
env = QT_QPA_PLATFORM,wayland  
env = ELECTRON_OZONE_PLATFORM_HINT,auto  
env = QT_QPA_PLATFORMTHEME,gtk3  
env = QT_QPA_PLATFORMTHEME_QT6,gtk3
```

#### Layer Rules[​](#layer-rules-1 "Direct link to Layer Rules")

```
layerrule = noanim, ^(dms)$
```

For more about layer rules see [layer rules](/docs/dankmaterialshell/layers).

#### General Layout[​](#general-layout "Direct link to General Layout")

```
general {  
    gaps_in = 5  
    gaps_out = 5  
    border_size = 0  
  
    col.active_border = rgba(707070ff)  
    col.inactive_border = rgba(d0d0d0ff)  
  
    layout = dwindle  
}
```

#### Decoration[​](#decoration "Direct link to Decoration")

```
decoration {  
    rounding = 12  
  
    active_opacity = 1.0  
    inactive_opacity = 0.9  
  
    shadow {  
        enabled = true  
        range = 30  
        render_power = 5  
        offset = 0 5  
        color = rgba(00000070)  
    }  
}
```

#### DMS Keybindings[​](#dms-keybindings-1 "Direct link to DMS Keybindings")

For the full list of available IPC commands see [IPC](/docs/dankmaterialshell/keybinds-ipc)

```
$mod = SUPER  
  
# Application Launchers  
bind = $mod, space, exec, dms ipc call spotlight toggle  
bind = $mod, V, exec, dms ipc call clipboard toggle  
bind = $mod, M, exec, dms ipc call processlist toggle  
bind = $mod, comma, exec, dms ipc call settings toggle  
bind = $mod, N, exec, dms ipc call notifications toggle  
bind = $mod, Y, exec, dms ipc call dankdash wallpaper  
bind = $mod, TAB, exec, dms ipc call hypr toggleOverview  
  
# Security  
bind = $mod ALT, L, exec, dms ipc call lock lock  
  
# Audio Controls  
bindel = , XF86AudioRaiseVolume, exec, dms ipc call audio increment 3  
bindel = , XF86AudioLowerVolume, exec, dms ipc call audio decrement 3  
bindl = , XF86AudioMute, exec, dms ipc call audio mute  
  
# Brightness Controls  
bindel = , XF86MonBrightnessUp, exec, dms ipc call brightness increment 5  
bindel = , XF86MonBrightnessDown, exec, dms ipc call brightness decrement 5
```

### Window Rules[​](#window-rules-1 "Direct link to Window Rules")

```
# Opacity for inactive windows  
windowrulev2 = opacity 0.9 0.9, floating:0, focus:0  
  
# GNOME apps  
windowrulev2 = rounding 12, class:^(org\.gnome\.)  
windowrulev2 = noborder, class:^(org\.gnome\.)  
  
# Terminal apps - no borders  
windowrulev2 = noborder, class:^(org\.wezfurlong\.wezterm)$  
windowrulev2 = noborder, class:^(Alacritty)$  
windowrulev2 = noborder, class:^(zen)$  
windowrulev2 = noborder, class:^(com\.mitchellh\.ghostty)$  
windowrulev2 = noborder, class:^(kitty)$  
  
# Floating windows  
windowrulev2 = float, class:^(gnome-calculator)$  
windowrulev2 = float, class:^(blueman-manager)$  
windowrulev2 = float, class:^(org\.gnome\.Nautilus)$
```

## Sway Configuration[​](#sway-configuration "Direct link to Sway Configuration")

[Sway](https://swaywm.org/) is an i3-compatible Wayland compositor. DankMaterialShell integrates with Sway's tiling layout.

### Key Configuration Sections[​](#key-configuration-sections-2 "Direct link to Key Configuration Sections")

Coming Soon

Detailed Sway configuration sections are coming soon. Sway configuration will include:

* Startup commands
* Environment variables
* DMS keybindings
* Layer rules
* Window rules

For now, refer to the [Example for Sway](#example-for-sway) in the "Other Compositors" section below for basic setup.

#### Startup[​](#startup-2 "Direct link to Startup")

Launch DankMaterialShell and optional services at compositor startup:

```
exec dms run  
exec wl-paste --watch cliphist store
```

#### DMS Keybindings[​](#dms-keybindings-2 "Direct link to DMS Keybindings")

For the full list of available IPC commands see [IPC](/docs/dankmaterialshell/keybinds-ipc). Basic Sway keybinding examples are available in the [Example for Sway](#example-for-sway) section below.

## dwl/MangoWC Configuration[​](#dwlmangowc-configuration "Direct link to dwl/MangoWC Configuration")

[MangoWC](https://github.com/DreamMaoMao/mangowc) is a dynamic tiling Wayland compositor based on dwl. DankMaterialShell integrates with MangoWC's tiling layout.

### Key Configuration Sections[​](#key-configuration-sections-3 "Direct link to Key Configuration Sections")

Coming Soon

Detailed MangoWC configuration sections are coming soon. MangoWC configuration will include:

* Startup commands
* Environment variables
* DMS keybindings
* Layer rules
* Window rules

For now, refer to the [MangoWC documentation](https://github.com/DreamMaoMao/mangowc) for basic setup.

#### Startup[​](#startup-3 "Direct link to Startup")

Launch DankMaterialShell and optional services at compositor startup. The exact syntax will be documented once configuration format is finalized.

#### DMS Keybindings[​](#dms-keybindings-3 "Direct link to DMS Keybindings")

For the full list of available IPC commands see [IPC](/docs/dankmaterialshell/keybinds-ipc). MangoWC keybinding configuration coming soon.

## Other Compositors[​](#other-compositors "Direct link to Other Compositors")

DankMaterialShell works with any Wayland compositor that supports:

* Layer shell protocol (for panels and overlays)
* Session lock protocol (for lock screen)

**Note:** Some compositor-specific features will be unavailable, such as workspace switching.

### Basic Integration[​](#basic-integration "Direct link to Basic Integration")

For other compositors, you need to:

1. **Auto-start DMS:**

   ```
   dms run
   ```
2. **Configure keybindings** using the IPC commands from the [Keybinds & IPC](/docs/dankmaterialshell/keybinds-ipc) guide
3. **Set environment variables:**

   ```
   export QT_QPA_PLATFORM=wayland
   ```

### Example for Sway[​](#example-for-sway "Direct link to Example for Sway")

Add to `~/.config/sway/config`:

```
# Startup  
exec dms run  
exec wl-paste --watch cliphist store  
  
# DMS Keybindings  
bindsym $mod+space exec dms ipc call spotlight toggle  
bindsym $mod+v exec dms ipc call clipboard toggle  
bindsym $mod+m exec dms ipc call processlist toggle  
bindsym $mod+comma exec dms ipc call settings toggle  
  
# Audio controls  
bindsym XF86AudioRaiseVolume exec dms ipc call audio increment 3  
bindsym XF86AudioLowerVolume exec dms ipc call audio decrement 3  
bindsym XF86AudioMute exec dms ipc call audio mute  
  
# Brightness controls  
bindsym XF86MonBrightnessUp exec dms ipc call brightness increment 5  
bindsym XF86MonBrightnessDown exec dms ipc call brightness decrement 5
```

## Troubleshooting[​](#troubleshooting "Direct link to Troubleshooting")

### DMS doesn't start automatically[​](#dms-doesnt-start-automatically "Direct link to DMS doesn't start automatically")

Check your compositor's logs to ensure the `exec-once` or equivalent startup command is running. You can also manually start DMS with `dms run` to see any error messages.

### Keybindings don't work[​](#keybindings-dont-work "Direct link to Keybindings don't work")

Verify that:

* DMS is running (`pgrep -f "dms run"`)
* Your keybinding syntax matches your compositor's format

## Next Steps[​](#next-steps "Direct link to Next Steps")

* Customize your shell appearance in [Themes](/docs/dankmaterialshell/application-themes)
* Explore all available IPC commands in [Keybinds & IPC](/docs/dankmaterialshell/keybinds-ipc)
* Add functionality with [Plugins](/docs/dankmaterialshell/plugins-overview)
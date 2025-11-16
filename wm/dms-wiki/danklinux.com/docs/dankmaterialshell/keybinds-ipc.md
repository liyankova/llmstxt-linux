---
source_url: "https://danklinux.com/docs/dankmaterialshell/keybinds-ipc"
title: "Keybinds & IPC | Dank Linux"
crawl_date: "2025-11-16T08:42:48.676719Z"
selector: "article"
---

# Keybinds & IPC | Dank Linux

* DankMaterialShell (dms)
* Keybinds & IPC

On this page

```
██████╗ ███╗   ███╗███████╗
██╔══██╗████╗ ████║██╔════╝
██║  ██║██╔████╔██║███████╗
██║  ██║██║╚██╔╝██║╚════██║
██████╔╝██║ ╚═╝ ██║███████║
╚═════╝ ╚═╝     ╚═╝╚══════╝
```

DankMaterialShell provides comprehensive IPC (Inter-Process Communication) functionality that allows external control of the shell through command-line commands. All IPC commands follow the format:

```
dms ipc call <target> <function> [parameters...]
```

## Core Controls[​](#core-controls "Direct link to Core Controls")

### audio[​](#audio "Direct link to audio")

Manage audio output and input devices.

| Function | Description | Parameters |
| --- | --- | --- |
| `setvolume <percentage>` | Set output volume | percentage (0-100) |
| `increment <step>` | Increase output volume | step (default: 5) |
| `decrement <step>` | Decrease output volume | step (default: 5) |
| `mute` | Toggle output mute | - |
| `setmic <percentage>` | Set microphone volume | percentage (0-100) |
| `micmute` | Toggle microphone mute | - |
| `status` | Get current audio status | - |

**Examples:**

```
dms ipc call audio setvolume 50  
dms ipc call audio increment 10  
dms ipc call audio mute
```

### brightness[​](#brightness "Direct link to brightness")

Control display brightness for internal and external displays.

| Function | Description | Parameters |
| --- | --- | --- |
| `set <percentage> [device]` | Set brightness level | percentage (1-100), device (optional) |
| `increment <step> [device]` | Increase brightness | step, device (optional) |
| `decrement <step> [device]` | Decrease brightness | step, device (optional) |
| `status` | Get current brightness status | - |
| `list` | List all brightness devices | - |
| `enableExponential [device]` | Enable exponential brightness mode | device (optional, uses current if not specified) |
| `disableExponential [device]` | Disable exponential brightness mode | device (optional, uses current if not specified) |
| `toggleExponential [device]` | Toggle exponential brightness mode | device (optional, uses current if not specified) |

**Examples:**

```
dms ipc call brightness set 80  
dms ipc call brightness increment 10 ""  
dms ipc call brightness decrement 5 "intel_backlight"  
dms ipc call brightness disableExponential "backlight:intel_backlight"  
dms ipc call brightness toggleExponential
```

### night[​](#night "Direct link to night")

Night mode (gamma/color temperature) control.

| Function | Description | Parameters |
| --- | --- | --- |
| `toggle` | Toggle night mode on/off | - |
| `enable` | Enable night mode | - |
| `disable` | Disable night mode | - |
| `status` | Get night mode status | - |
| `temperature [value]` | Get/set color temperature | value in Kelvin (2500-6000, optional) |
| `automation [mode]` | Get/set automation mode | "manual", "time", or "location" (optional) |
| `schedule <start> <end>` | Set time-based schedule | start time (HH:MM), end time (HH:MM) |
| `location <lat> <lon>` | Set location coordinates | latitude, longitude |

**Examples:**

```
dms ipc call night toggle  
dms ipc call night temperature 4000  
dms ipc call night automation time  
dms ipc call night schedule 20:00 06:00  
dms ipc call night location 40.7128 -74.0060
```

### mpris[​](#mpris "Direct link to mpris")

Media player control via MPRIS interface.

| Function | Description |
| --- | --- |
| `list` | List all available media players |
| `play` | Start playback |
| `pause` | Pause playback |
| `playPause` | Toggle play/pause |
| `previous` | Skip to previous track |
| `next` | Skip to next track |
| `stop` | Stop playback |

**Examples:**

```
dms ipc call mpris playPause  
dms ipc call mpris next
```

### lock[​](#lock "Direct link to lock")

Screen lock control and status.

| Function | Description |
| --- | --- |
| `lock` | Lock the screen immediately |
| `demo` | Show lock screen demo (doesn't lock) |
| `isLocked` | Check if screen is locked |

**Examples:**

```
dms ipc call lock lock  
dms ipc call lock isLocked
```

### inhibit[​](#inhibit "Direct link to inhibit")

Idle inhibitor control to prevent automatic sleep/lock.

| Function | Description |
| --- | --- |
| `toggle` | Toggle idle inhibit state |
| `enable` | Enable idle inhibit (prevent sleep) |
| `disable` | Disable idle inhibit (allow sleep) |

**Examples:**

```
dms ipc call inhibit toggle  
dms ipc call inhibit enable
```

## Wallpaper & Profile[​](#wallpaper--profile "Direct link to Wallpaper & Profile")

### wallpaper[​](#wallpaper "Direct link to wallpaper")

Wallpaper management with support for global and per-monitor configurations.

#### Global Wallpaper Functions[​](#global-wallpaper-functions "Direct link to Global Wallpaper Functions")

| Function | Description | Parameters |
| --- | --- | --- |
| `get` | Get current wallpaper path | - |
| `set <path>` | Set wallpaper | path to image file |
| `clear` | Clear all wallpapers | - |
| `next` | Cycle to next wallpaper | - |
| `prev` | Cycle to previous wallpaper | - |

#### Per-Monitor Functions[​](#per-monitor-functions "Direct link to Per-Monitor Functions")

| Function | Description | Parameters |
| --- | --- | --- |
| `getFor <screen>` | Get wallpaper for monitor | monitor name (e.g., "DP-2") |
| `setFor <screen> <path>` | Set wallpaper for monitor | monitor name, path to image |
| `nextFor <screen>` | Cycle to next wallpaper | monitor name |
| `prevFor <screen>` | Cycle to previous wallpaper | monitor name |

**Examples:**

```
# Global wallpaper mode  
dms ipc call wallpaper set /path/to/image.jpg  
dms ipc call wallpaper next  
  
# Per-monitor wallpaper mode  
dms ipc call wallpaper setFor DP-2 /path/to/image1.jpg  
dms ipc call wallpaper setFor eDP-1 /path/to/image2.jpg  
dms ipc call wallpaper nextFor eDP-1  
  
# Clear and return to global mode  
dms ipc call wallpaper clear
```

**Note:** When per-monitor mode is enabled, legacy global functions will return error messages directing you to use the per-monitor equivalents.

### profile[​](#profile "Direct link to profile")

User profile image management.

| Function | Description | Parameters |
| --- | --- | --- |
| `getImage` | Get current profile image path | - |
| `setImage <path>` | Set profile image | path to image file |
| `clearImage` | Clear profile image | - |

**Examples:**

```
dms ipc call profile setImage /path/to/avatar.png  
dms ipc call profile clearImage
```

## Appearance Controls[​](#appearance-controls "Direct link to Appearance Controls")

### theme[​](#theme "Direct link to theme")

Theme mode control (light/dark mode switching).

| Function | Description |
| --- | --- |
| `toggle` | Toggle between light and dark themes |
| `light` | Switch to light theme |
| `dark` | Switch to dark theme |
| `getMode` | Get current theme mode |

**Examples:**

```
dms ipc call theme toggle  
dms ipc call theme dark
```

### bar[​](#bar "Direct link to bar")

Top bar visibility control.

| Function | Description |
| --- | --- |
| `reveal` | Show the top bar |
| `hide` | Hide the top bar |
| `toggle` | Toggle top bar visibility |
| `status` | Get visibility status |

**Examples:**

```
dms ipc call bar toggle  
dms ipc call bar hide
```

### dock[​](#dock "Direct link to dock")

Dock visibility control.

| Function | Description |
| --- | --- |
| `reveal` | Show the dock |
| `hide` | Hide the dock |
| `toggle` | Toggle dock visibility |

**Examples:**

```
dms ipc call dock toggle  
dms ipc call dock hide  
dms ipc call dock reveal
```

## Modal Controls[​](#modal-controls "Direct link to Modal Controls")

These targets control various modal windows and overlays.

### spotlight[​](#spotlight "Direct link to spotlight")

Application launcher modal with search capabilities.

| Function | Description | Parameters |
| --- | --- | --- |
| `open` | Show launcher | - |
| `close` | Hide launcher | - |
| `toggle` | Toggle launcher visibility | - |
| `openQuery <query>` | Show launcher with search | search text |
| `toggleQuery <query>` | Toggle launcher with search | search text |

**Examples:**

```
dms ipc call spotlight toggle  
dms ipc call spotlight openQuery browser  
dms ipc call spotlight toggleQuery "!"
```

### Other Modals[​](#other-modals "Direct link to Other Modals")

All these modals support `open`, `close`, and `toggle` functions:

* **clipboard** - Clipboard history manager
* **notifications** - Notification center
* **settings** - Settings modal
* **processlist** - System process list and performance monitor
* **powermenu** - Power menu for system actions
* **control-center** - Quick settings (network, bluetooth, audio, etc.)
* **notepad** - Quick notepad/scratchpad

**Examples:**

```
dms ipc call clipboard toggle  
dms ipc call notifications open  
dms ipc call settings toggle  
dms ipc call processlist open  
dms ipc call powermenu toggle  
dms ipc call control-center toggle  
dms ipc call notepad open
```

### dash[​](#dash "Direct link to dash")

Dashboard popup with multiple tabs.

| Function | Description | Parameters |
| --- | --- | --- |
| `open [tab]` | Show dashboard | tab: "", "overview", "media", "weather" |
| `close` | Hide dashboard | - |
| `toggle [tab]` | Toggle dashboard | tab |

**Examples:**

```
dms ipc call dash toggle ""  
dms ipc call dash open overview  
dms ipc call dash toggle media  
dms ipc call dash open weather
```

### file[​](#file "Direct link to file")

File browser controls for selecting wallpapers and profile images.

| Function | Description | Parameters |
| --- | --- | --- |
| `browse <type>` | Open file browser | "wallpaper" or "profile" |

**Examples:**

```
dms ipc call file browse wallpaper  
dms ipc call file browse profile
```

### dankdash[​](#dankdash "Direct link to dankdash")

DankDash wallpaper browser control.

| Function | Description |
| --- | --- |
| `wallpaper` | Toggle DankDash wallpaper browser |

**Examples:**

```
dms ipc call dankdash wallpaper
```

## System Utilities[​](#system-utilities "Direct link to System Utilities")

### niri[​](#niri "Direct link to niri")

**Requires niri newer than 25.08**

Screenshot functionality for the niri compositor. Captures are opened in your configured editor for markup and annotation.

| Function | Description |
| --- | --- |
| `screenshot` | Interactive selection screenshot |
| `screenshotScreen` | Capture entire screen |
| `screenshotWindow` | Capture focused window |

**Examples:**

```
dms ipc call niri screenshot  
dms ipc call niri screenshotScreen  
dms ipc call niri screenshotWindow
```

**Configuration:**

Set the `DMS_SCREENSHOT_EDITOR` environment variable to choose your preferred screenshot editor backend:

```
# Use Swappy (default)  
export DMS_SCREENSHOT_EDITOR=swappy  
  
# Use Satty  
export DMS_SCREENSHOT_EDITOR=satty
```

**Requirements:** niri compositor and your chosen screenshot editor (Swappy or Satty) must be installed.

### keybinds[​](#keybinds "Direct link to keybinds")

Dynamic keybinds cheatsheet modal that works with multiple providers.

| Function | Description | Parameters |
| --- | --- | --- |
| `open <provider>` | Show keybinds modal | provider name (e.g., "hyprland", "sway", "mangowc") |
| `openWithPath <provider> <path>` | Show keybinds modal with custom config path | provider name, path to config |
| `close` | Hide keybinds modal | - |
| `toggle <provider>` | Toggle keybinds modal visibility | provider name |
| `toggleWithPath <provider> <path>` | Toggle keybinds modal with custom config path | provider name, path to config |

**Examples:**

```
dms ipc call keybinds toggle hyprland  
dms ipc call keybinds toggle sway  
dms ipc call keybinds toggle mangowc  
dms ipc call keybinds open tmux  
  
# With custom config paths  
dms ipc call keybinds openWithPath hyprland /custom/path/to/hypr  
dms ipc call keybinds toggleWithPath sway /etc/sway/config
```

**Supported Providers:**

The keybinds modal supports all providers available through the `dms keybinds` CLI:

* **Built-in providers**: Hyprland, Sway, MangoWC (automatically parse compositor configs)
* **Custom cheatsheets**: Any JSON-based cheatsheet in `~/.config/DankMaterialShell/cheatsheets/`

The modal automatically parses configuration files and displays keybinds organized by category with optional subcategories. See the [Keybinds & Cheatsheets](/docs/dankmaterialshell/cli-keybinds-cheatsheets) documentation for more details on providers and creating custom cheatsheets.

### hypr[​](#hypr "Direct link to hypr")

**Hyprland-only features**

Hyprland-specific workspace overview control.

| Function | Description |
| --- | --- |
| `openOverview` | Show Hyprland workspace overview |
| `closeOverview` | Hide Hyprland workspace overview |
| `toggleOverview` | Toggle Hyprland workspace overview visibility |

**Examples:**

```
dms ipc call hypr toggleOverview
```

**Workspace Overview:**

The workspace overview shows all your workspaces across all monitors with live window previews:

* **Multi-monitor support** - Shows workspaces from all connected monitors with monitor name labels
* **Live window previews** - Real-time screen capture of all windows on each workspace
* **Drag-and-drop** - Move windows between workspaces and monitors by dragging
* **Keyboard navigation** - Use Left/Right arrow keys to switch between workspaces on current monitor
* **Visual indicators** - Active workspace highlighted when it contains windows
* **Click to switch** - Click any workspace to switch to it
* **Click outside or press Escape** - Close the overview

**Note:** All hypr functions return `HYPR_NOT_AVAILABLE` if not running Hyprland.

### systemupdater[​](#systemupdater "Direct link to systemupdater")

System updater external check request.

| Function | Description |
| --- | --- |
| `updatestatus` | Trigger system update check |

**Examples:**

```
dms ipc call systemupdater updatestatus
```

## Scripting and Automation[​](#scripting-and-automation "Direct link to Scripting and Automation")

IPC commands are designed for integration with keybindings, scripts, and automation tools.

### Time-based Automation[​](#time-based-automation "Direct link to Time-based Automation")

```
#!/bin/bash  
# Toggle night mode based on time of day  
hour=$(date +%H)  
if [ $hour -ge 20 ] || [ $hour -le 6 ]; then  
    dms ipc call night enable  
else  
    dms ipc call night disable  
fi
```

### Status Checking[​](#status-checking "Direct link to Status Checking")

```
# Check if screen is locked before performing action  
if dms ipc call lock isLocked | grep -q "false"; then  
    dms ipc call notifications open  
fi
```

### Conditional Logic[​](#conditional-logic "Direct link to Conditional Logic")

```
# Increase brightness only if below threshold  
current=$(dms ipc call brightness status | grep -oP '\d+')  
if [ "$current" -lt 50 ]; then  
    dms ipc call brightness set 50  
fi
```

## Return Values[​](#return-values "Direct link to Return Values")

Most IPC functions return string messages indicating:

* Success confirmation with current values
* Error messages if operation fails
* Status information for query functions
* Empty/void return for simple action functions

Functions that return void (like media controls) execute the action but don't provide feedback. Check the application state through other means if needed.

## Next Steps[​](#next-steps "Direct link to Next Steps")

See compositor-specific keybinding configuration in your compositor's documentation to integrate these IPC commands with your workflow.
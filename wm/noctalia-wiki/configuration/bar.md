---
source_url: "https://docs.noctalia.dev/configuration/bar/"
title: "Bar & Bar widgets | Noctalia Docs"
crawl_date: "2025-11-16T08:47:15.334878Z"
selector: "main"
---

# Bar & Bar widgets | Noctalia Docs

# Bar & Bar widgets

## Bar

[Section titled “Bar”](#bar)

**Customize the bar’s appearance and position.**

```
"bar": {

"position": "top",

"backgroundOpacity": 1,

"monitors": [],

"density": "default",

"showCapsule": true,

"floating": false,

"marginVertical": 0.25,

"marginHorizontal": 0.25,

"widgets": {

"left": [

// Widgets

],

"center": [

// Widgets

],

"right": [

// Widgets

]

}

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| position | `"top"` | `"bottom"` , `"top"` , `"right"` , `"left"` | Choose where to place the bar on the screen. |
| backgroundOpacity | `1` | 0.00 to 1.00 with 0.01 steps | Adjust the background opacity of the bar. |
| monitors | blank, therefore all monitors | See note on monitors | Show bar on specific monitors. Defaults to all if none are chosen. |
| density | `"default"` | `"mini"` , `"compact"` , `"comfortable"` , `"default"` | Adjust the bar’s padding for a compact or spacious look. |
| showCapsule | true | boolean | Show widget backgrounds. |
| floating | false | boolean | Displays the bar as a floating ‘pill’. Note: This will move the screen corners to the edges. |
| marginVertical | 0.25 | 0.00 to 1.00 with 0.01 steps | Adjust the vertical margin around the floating bar. |
| marginHorizontal | 0.25 | 0.00 to 1.00 with 0.01 steps | Adjust the horizontal margin around the floating bar. |

**Note on monitors:**

You can determine your monitor identifiers from:

Hyprland:

Terminal window

```
hyprctl monitors
```

Niri:

Terminal window

```
niri msg outputs
```

## Widgets

[Section titled “Widgets”](#widgets)

### Default widgets

[Section titled “Default widgets”](#default-widgets)

All widgets can be placed in either `"left"`, `"center"` or `"right"`.

Expand this section to see the defaults widgets

```
"widgets": {

"left": [

{

"id": "SystemMonitor"

},

{

"id": "ActiveWindow"

},

{

"id": "MediaMini"

}

],

"center": [

{

"id": "Workspace"

}

],

"right": [

{

"id": "ScreenRecorder"

},

{

"id": "Tray"

},

{

"id": "NotificationHistory"

},

{

"id": "Battery"

},

{

"id": "Volume"

},

{

"id": "Brightness"

},

{

"id": "Clock"

},

{

"id": "ControlCenter"

}

]

}
```

### ActiveWindow

[Section titled “ActiveWindow”](#activewindow)

Displays the title and icon of the current active window.

```
{

"id": "ActiveWindow",

"showIcon": true,

"hideMode": "hidden",

"scrollingMode": "hover",

"width": 145,

"colorizeIcons": false

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| showIcon | true | boolean | Show the icon of the active window |
| hideMode | `"hidden"` | `"visible"` , `"hidden"` , `"transparent"` | ”visible”: Always Visible, “hidden”: Hide When Empty, “transparent”: Transparent When Empty. |
| scrollingMode | `"hover"` | `"never"` , `"always"` , `"hover"` | When should long titles scroll to show more of the title. |
| width | 145 | Integer value in pixels | Controls the horizontal size of the widget. |
| colorizeIcons | false | boolean | Show original window icon if false or colorize (match theme) if true. |

### Battery

[Section titled “Battery”](#battery)

Displays battery percentage.

```
{

"id": "Battery",

"displayMode": "onhover",

"warningThreshold": 30

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| displayMode | `"onhover"` | `"onhover"` , `"alwaysShow"` , `"alwaysHide"` | Whether to always show battery percentage, or only on hover. |
| warningThreshold | `30` | Integer values between 0 to 100 | At what percentage to warn of low battery. |

### Bluetooth

[Section titled “Bluetooth”](#bluetooth)

Access Bluetooth popup for devices and adapter.

```
{

"id": "Bluetooth"

}
```

No further settings.

### Brightness

[Section titled “Brightness”](#brightness)

Displays the laptop brightness percentage.

```
{

"id": "Brightness",

"displayMode": "onhover"

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| displayMode | `"onhover"` | `"onhover"` , `"alwaysShow"` , `"alwaysHide"` | Whether to always show the laptop brightness percentage, or only on hover. |

### Clock

[Section titled “Clock”](#clock)

Displays time, date or other time related information of your choosing, with a calendar upon left click.

```
{

"id": "Clock",

"usePrimaryColor": true,

"useCustomFont": false,

"customFont": "",

"formatHorizontal": "HH:mm ddd, MMM dd",

"formatVertical": "HH mm - dd MM"

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| usePrimaryColor | true | boolean | When enabled, this applies the primary color for emphasis. |
| useCustomFont | false | boolean | Override the default font selection with a custom font for the clock. |
| customFont | `""` | String of a installed font name. | Select a custom font for the clock display. |
| formatHorizontal | `"HH:mm ddd, MMM dd"` | String of QTime formatting. See note on QTime formatting | Format the Clock for when the bar is horizontal. |
| formatVertical | `"HH mm - dd MM"` | String of QTime formatting. See note on QTime formatting | Format the Clock for when the bar is vertical. |

**Note on QTime formatting:**

Clock uses the [QTime formatting](https://doc.qt.io/qt-6/qtime.html#toString-1)

### ControlCenter

[Section titled “ControlCenter”](#controlcenter)

Adds an icon-button to open the ControlCenter menu.

```
{

"id": "ControlCenter",

"useDistroLogo": false,

"icon": "noctalia",

"customIconPath": ""

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| useDistroLogo | false | boolean | When enabled, the distro logo will be used as icon. |
| icon | `"noctalia"` | String of icon name | Choose an icon by name. |
| customIconPath | `""` | String of icon path | Manually link to a custom icon. |

### CustomButton

[Section titled “CustomButton”](#custombutton)

Adds a custom button that can be configured to execute commands and display command returns.

```
{

"id": "CustomButton",

"icon": "heart",

"leftClickExec": "",

"rightClickExec": "",

"middleClickExec": "",

"textCommand": "",

"textIntervalMs": 3000

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| icon | `"heart"` | String of icon name | Choose a icon by name. |
| leftClickExec | `""` | String of command | Command to execute when the button is left-clicked. |
| rightClickExec | `""` | String of command | Command to execute when the button is right-clicked. |
| middleClickExec | `""` | String of command | Command to execute when the button is middle-clicked. |
| textCommand | `""` | String of command | The return of this command will be displayed by the widget. |
| textIntervalMs | 3000 | Integer values in milliseconds | The time delay between executing the *textCommand* command. |

### DarkMode

[Section titled “DarkMode”](#darkmode)

Adds a button to toggle dark mode.

```
{

"id": "DarkMode"

}
```

No further settings.

### KeepAwake

[Section titled “KeepAwake”](#keepawake)

Adds a button to toggle keep awake mode.

```
{

"id": "KeepAwake"

}
```

No further settings.

### KeyboardLayout

[Section titled “KeyboardLayout”](#keyboardlayout)

Adds a button to toggle between keyboard layouts.

```
{

"id": "KeyboardLayout",

"displayMode": "onhover"

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| displayMode | `"onhover"` | `"onhover"` , `"forceOpen"` , `"alwaysHide"` | Whether to always show the active keyboard layout, or only on hover. |

### MediaMini

[Section titled “MediaMini”](#mediamini)

Display a media-player widget with animations.

```
{

"id": "MediaMini",

"hideMode": "hidden",

"scrollingMode": "hover",

"maxWidth": 145,

"useFixedWidth": false,

"showAlbumArt": false,

"showVisualizer": false,

"visualizerType": "linear"

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| hideMode | `"hidden"` | `"visible"` , `"hidden"` , `"transparent"` | Whether to always show the widget, hide it, or make it transparent when empty. |
| scrollingMode | `"hover"` | `"never"` , `"always"` , `"hover"` | Control when text scrolling is enabled for long track titles. |
| maxWidth | 145 | Integer values in pixels | Sets the maximum horizontal size of the widget. The widget will shrink to fit shorter content. |
| useFixedWidth | false | boolean | When enabled, the widget will always use the maximum width instead of dynamically adjusting to content. |
| showAlbumArt | false | boolean | Display the album artwork for the currently playing track. |
| showVisualizer | false | boolean | Display an audio visualizer when music is playing. |
| visualizerType | `"linear"` | `"linear"` , `"mirrored"` , `"wave"` | Choose the style of audio visualizer to display. |

### Microphone

[Section titled “Microphone”](#microphone)

Mute or control the volume of the microphone.

```
{

"id": "Microphone",

"displayMode": "onhover"

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| displayMode | `"onhover"` | `"onhover"` , `"alwaysShow"` , `"alwaysHide"` | Whether to always show the microphone volume percentage, or only on hover. |

### NightLight

[Section titled “NightLight”](#nightlight)

Adds a button to toggle Night Light mode.

```
{

"id": "NightLight"

}
```

No further settings.

### NotificationHistory

[Section titled “NotificationHistory”](#notificationhistory)

Adds a button to show notifications or toggle *Do not disturb* mode.

```
{

"id": "NotificationHistory",

"showUnreadBadge": true,

"hideWhenZero": true

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| showUnreadBadge | true | boolean | Display a badge showing the number of unread notifications. |
| hideWhenZero | true | boolean | Hide the notification badge when there are no unread notifications. |

### PowerProfile

[Section titled “PowerProfile”](#powerprofile)

Adds a button to switch between Power-profiles.

```
{

"id": "PowerProfile"

}
```

No further settings.

### ScreenRecorder

[Section titled “ScreenRecorder”](#screenrecorder)

Adds a button to start and stop screen recordings.

```
{

"id": "ScreenRecorder"

}
```

No further settings.

### SessionMenu

[Section titled “SessionMenu”](#sessionmenu)

Adds a button to open the sessions menu.

```
{

"id": "SessionMenu"

}
```

No further settings.

### Spacer

[Section titled “Spacer”](#spacer)

Adds a spacer.

```
{

"id": "Spacer",

"width": 20

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| width | 20 | Integer value in pixels | Spacing width in pixels. |

### SystemMonitor

[Section titled “SystemMonitor”](#systemmonitor)

Show information about the system, like CPU, RAM and disk usage, as well as CPU temperature.

```
{

"id": "SystemMonitor",

"showCpuUsage": true,

"showCpuTemp": true,

"showMemoryUsage": true,

"showMemoryAsPercent": false,

"showNetworkStats": false,

"showDiskUsage": false

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| showCpuUsage | true | boolean | Display current CPU usage percentage. |
| showCpuTemp | true | boolean | Show CPU temperature readings if available. |
| showMemoryUsage | true | boolean | Display current RAM usage information. |
| showMemoryAsPercent | false | boolean | Show memory usage as a percentage instead of absolute values. |
| showNetworkStats | false | boolean | Display network upload and download speeds. |
| showDiskUsage | false | boolean | Show disk space usage information. |

### Taskbar

[Section titled “Taskbar”](#taskbar)

Show and access open applications.

```
{

"id": "Taskbar",

"onlySameOutput": true,

"onlyActiveWorkspaces": true,

"hideMode": "hidden",

"colorizeIcons": false

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| onlySameOutput | true | boolean | Show only apps from the output where the bar is located. |
| onlyActiveWorkspaces | true | boolean | Show only apps from active workspaces. |
| hideMode | `"hidden"` | `"visible"` , `"hidden"` , `"transparent"` | Whether to always show the widget, hide it, or make it transparent when empty. |
| colorizeIcons | false | boolean | Apply theme colors to taskbar icons. |

### Tray

[Section titled “Tray”](#tray)

Show and access open applications.

```
{

"id": "Tray",

"blacklist": [],

"colorizeIcons": false

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| blacklist | blank, therefore all tray icons are shown | See note on applications | Hide listed tray icons. Exclusion rules support wildcards (\*). |
| colorizeIcons | false | boolean | Apply theme colors to tray icons. |

**Note on applications:**

If you have a tray icon you want to hide, hover over the icon in the icon tray, note down the name, and input it as a string in the `"blacklist"` list. Example for hiding the Remmina tray icon:

```
{

"id": "Tray",

"blacklist": [ "remmina-icon" ],

"colorizeIcons": false

}
```

### Volume

[Section titled “Volume”](#volume)

Mute or control the volume of the active audio device.

```
{

"id": "Volume",

"displayMode": "onhover"

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| displayMode | `"onhover"` | `"onhover"` , `"alwaysShow"` , `"alwaysHide"` | Whether to always show the volume percentage, or only on hover. |

### WiFi

[Section titled “WiFi”](#wifi)

Adds a button to access the WiFi menu.

```
{

"id": "WiFi",

"displayMode": "onhover"

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| displayMode | `"onhover"` | `"onhover"` , `"alwaysShow"` , `"alwaysHide"` | Whether to always show the SSID of the connected WiFi network, only on hover or to always hide. |

### WallpaperSelector

[Section titled “WallpaperSelector”](#wallpaperselector)

Adds a button to open the Wallpaper manager.

```
{

"id": "WallpaperSelector"

}
```

No further settings.

### Workspace

[Section titled “Workspace”](#workspace)

View and access workspaces.

```
{

"id": "Workspace",

"labelMode": "index",

"hideUnoccupied": false,

"characterCount": 2

}
```

| Settings | Default | Options | Description |
| --- | --- | --- | --- |
| labelMode | `"index"` | `"none"` , `"name"` , `"index"` | Choose how workspace labels are displayed. |
| hideUnoccupied | false | boolean | Whether to display workspaces without windows. |
| characterCount | 2 | number | Number of characters shown from the workspace name. |
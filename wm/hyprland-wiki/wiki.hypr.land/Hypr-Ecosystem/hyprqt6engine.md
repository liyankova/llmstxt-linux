---
source_url: "https://wiki.hypr.land/Hypr-Ecosystem/hyprqt6engine/"
title: "hyprqt6engine – Hyprland Wiki"
crawl_date: "2025-11-21T17:57:45.411780Z"
selector: "article"
---

# hyprqt6engine – Hyprland Wiki

[Hypr Ecosystem](/Hypr-Ecosystem/)

hyprqt6engine

# hyprqt6engine

[hyprqt6engine](https://github.com/hyprwm/hyprqt6engine) provides a theme for QT6 apps. It’s a replacement for qt6ct, compatible with KDE Apps / KColorScheme.

## Usage

Install, then set `QT_QPA_PLATFORMTHEME=hyprqt6engine`.  
You can set this as `env=` in Hyprland, or in `/etc/environment` for setting it system-wide.

## Configuration

The config file is located in `~/.config/hypr/hyprqt6engine.conf`.

### Theme

category `theme:`

| Variable | Description | Type | Default |
| --- | --- | --- | --- |
| `color_scheme` | The full path to a color scheme. Can be a qt6ct theme, or a KColorScheme. Leave empty for defaults. | string | *empty* |
| `icon_theme` | Name of an icon theme to use. | string | *empty* |
| `style` | Widget style to use, e.g. Fusion or kvantum-dark. | string | `Fusion` |
| `font_fixed` | Font family for the fixed width font. | string | `monospace` |
| `font_fixed_size` | Font size for the fixed width font. | int | `11` |
| `font` | Font family for the regular font. | string | `Sans Serif` |
| `font_size` | Font size for the regular font. | int | `11` |

### Misc

category `misc:`

| Variable | Description | Type | Default |
| --- | --- | --- | --- |
| `single_click_activate` | Whether single-clicks should activate, or open. | bool | `true` |
| `menus_have_icons` | Whether context menus should include icons. | bool | `true` |
| `shortcuts_for_context_menus` | Whether context menu options should show their keyboard shortcuts. | bool | `true` |

Last updated on November 20, 2025

[hyprland-qt-support](/Hypr-Ecosystem/hyprland-qt-support/ "hyprland-qt-support")[hyprcursor](/Hypr-Ecosystem/hyprcursor/ "hyprcursor")
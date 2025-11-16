---
source_url: "https://danklinux.com/docs/dankmaterialshell/application-themes"
title: "Application Theming | Dank Linux"
crawl_date: "2025-11-16T08:42:29.723805Z"
selector: "article"
---

# Application Theming | Dank Linux

* DankMaterialShell (dms)
* Themes
* Application Theming

On this page

```
████████╗██╗  ██╗███████╗███╗   ███╗███████╗███████╗
╚══██╔══╝██║  ██║██╔════╝████╗ ████║██╔════╝██╔════╝
   ██║   ███████║█████╗  ██╔████╔██║█████╗  ███████╗
   ██║   ██╔══██║██╔══╝  ██║╚██╔╝██║██╔══╝  ╚════██║
   ██║   ██║  ██║███████╗██║ ╚═╝ ██║███████╗███████║
   ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝     ╚═╝╚══════╝╚══════╝
```

DankMaterialShell automatically generates theme files for native applications when matugen is enabled. These files are created on wallpaper changes and theme switches.

## Disabling Matugen[​](#disabling-matugen "Direct link to Disabling Matugen")

Set the environment variable before launching to disable theme generation entirely:

```
export DMS_DISABLE_MATUGEN=1  
dms run
```

## Custom Matugen Templates[​](#custom-matugen-templates "Direct link to Custom Matugen Templates")

You can add your own matugen templates to theme additional applications. Templates must use absolute paths and be defined under the `[config]` section. DMS will execute these templates alongisde its built-in templates.

See the [matugen wiki](https://github.com/InioX/matugen/wiki/Configuration) for full configuration and templating options.

Create or edit `~/.config/matugen/config.toml`:

```
[config]  
  
[templates.mytemplate]  
input_path = '/home/username/.config/matugen/templates/mytemplate.toml'  
output_path = '/home/username/.local/share/mytemplate/themes/matugen.toml'  
  
[templates.myapp]  
input_path = '/home/username/.config/matugen/templates/myapp.conf'  
output_path = '/home/username/.config/myapp/colors.conf'
```

**Important notes:**

* Use absolute paths, not relative paths like `./templates/`
* All template definitions must be under the `[config]` section
* Templates will regenerate on wallpaper changes and theme switches

## Generated Files[​](#generated-files "Direct link to Generated Files")

When matugen is enabled, theme files are always generated regardless of the "Apply GTK/Qt Themes" toggle:

* `~/.config/gtk-3.0/dank-colors.css`
* `~/.config/gtk-4.0/dank-colors.css`
* `~/.config/qt5ct/colors/matugen.conf`
* `~/.config/qt6ct/colors/matugen.conf`

The "Apply GTK/Qt Themes" toggles only control whether DankMaterialShell manages the symlinks to make applications use these files.

## GTK Applications[​](#gtk-applications "Direct link to GTK Applications")

### Install Prerequisites[​](#install-prerequisites "Direct link to Install Prerequisites")

```
# Arch  
sudo pacman -S adw-gtk-theme  
  
# Fedora  
sudo dnf install adw-gtk3-theme
```

### Enable via Settings[​](#enable-via-settings "Direct link to Enable via Settings")

1. Open **Settings → Theme & Colors**
2. Toggle **Apply GTK Themes**

This creates symlinks from `dank-colors.css` to `gtk.css`, enabling dynamic theming for GTK 3 and GTK 4 applications.

### Manual Integration[​](#manual-integration "Direct link to Manual Integration")

If you manage your own GTK theme but want DMS colors:

```
/* In ~/.config/gtk-3.0/gtk.css or gtk-4.0/gtk.css */  
@import url("dank-colors.css");
```

## Qt Applications[​](#qt-applications "Direct link to Qt Applications")

Qt theming offers two approaches: basic GTK passthrough or dedicated Qt control.

### Option 1: GTK Passthrough (Simple)[​](#option-1-gtk-passthrough-simple "Direct link to Option 1: GTK Passthrough (Simple)")

Best for users who primarily run GTK applications. Qt apps will use the GTK theme.

**niri Configuration:**

```
environment {  
  QT_QPA_PLATFORMTHEME "gtk3"  
  QT_QPA_PLATFORMTHEME_QT6 "gtk3"  
}
```

**Hyprland Configuration:**

```
env = QT_QPA_PLATFORMTHEME,gtk3  
env = QT_QPA_PLATFORMTHEME_QT6,gtk3
```

### Option 2: Dedicated Qt Control (Advanced)[​](#option-2-dedicated-qt-control-advanced "Direct link to Option 2: Dedicated Qt Control (Advanced)")

Provides better Qt integration and more styling control.

**Install qt6ct:**

```
# Arch  
paru -S qt6ct-kde  
  
# Fedora  
sudo dnf install qt6ct  
  
# Other distributions  
# Follow instructions at https://www.opencode.net/trialuser/qt6ct
```

**Configure Environment:**

**niri:**

```
environment {  
  QT_QPA_PLATFORMTHEME "qt6ct"  
  QT_QPA_PLATFORMTHEME_QT6 "qt6ct"  
}
```

**Hyprland:**

```
env = QT_QPA_PLATFORMTHEME,qt6ct  
env = QT_QPA_PLATFORMTHEME_QT6,qt6ct
```

**Enable Qt Theming:**

1. Restart your compositor session for environment changes to take effect
2. Open **Settings → Theme & Colors**
3. Toggle **Apply Qt Themes**

This links the generated matugen color files to qt5ct/qt6ct configurations.

## Firefox[​](#firefox "Direct link to Firefox")

Firefox has two theme integration options: Material Fox or Pywalfox.

### Option 1: Material Fox (Chrome-like with Dynamic Colors)[​](#option-1-material-fox-chrome-like-with-dynamic-colors "Direct link to Option 1: Material Fox (Chrome-like with Dynamic Colors)")

Firefox uses GTK3 theming but a separate matugen CSS is generated for better integration with Material Fox.

**Enable Custom Styles in Firefox:**

Navigate to `about:config` and set:

* `toolkit.legacyuserprofilecustomizations.stylesheets` = `true`
* `svg.context-properties.content.enabled` = `true`

Create new boolean property:

* `userChrome.theme-material` = `true`

**Install Material Fox Theme:**

```
# Find Firefox profile directory  
export PROFILE_DIR=$(find ~/.mozilla/firefox -maxdepth 1 -type d -name "*.default-release" | head -n 1)  
  
# Download and extract theme  
curl -L -o "$PROFILE_DIR/chrome.zip" https://github.com/edelvarden/material-fox-updated/releases/download/v2.0.0/chrome.zip  
unzip -o "$PROFILE_DIR/chrome.zip" -d "$PROFILE_DIR"  
rm "$PROFILE_DIR/chrome.zip"
```

**Link Dynamic Colors:**

```
export PROFILE_DIR=$(find ~/.mozilla/firefox -maxdepth 1 -type d -name "*.default-release" | head -n 1)  
rm -f "$PROFILE_DIR/chrome/theme-material-blue.css"  
ln -sf ~/.config/DankMaterialShell/firefox.css "$PROFILE_DIR/chrome/theme-material-blue.css"
```

Restart Firefox to apply changes.

### Option 2: Pywalfox[​](#option-2-pywalfox "Direct link to Option 2: Pywalfox")

**Install Pywalfox:**

```
# Arch  
paru -S python-pywalfox  
  
# Other distributions  
# Install from https://github.com/Frewacom/pywalfox
```

**Install Browser Extension:**

Install the [Pywalfox extension](https://addons.mozilla.org/firefox/addon/pywalfox/) from Firefox Add-ons.

**Enable DMS Colors:**

```
ln -sf ~/.cache/wal/dank-pywalfox.json ~/.cache/wal/colors.json
```

Restart DMS to generate the palette, then enable Pywalfox in the browser.

### Browser Tips[​](#browser-tips "Direct link to Browser Tips")

* Keep userChrome/userContent overrides under version control
* Disable conflicting theme extensions when using DMS-managed colors

## Editors[​](#editors "Direct link to Editors")

Editors use a mix of `dank16` and matugen to produce a colorful, theme-honoring template with contrast in the editor itself.

### VSCode/VSCodium/VSCode-oss[​](#vscodevscodiumvscode-oss "Direct link to VSCode/VSCodium/VSCode-oss")

Open the command palette with `ctrl`+`shift`+`p`, choose `Preferences: Color Scheme` and then pick `Dynamic Base16 DankShell`

![VS Code theme selection](/img/vscodelight.png)![VS Code theme selection](/img/vscode.png)

## Terminal Applications[​](#terminal-applications "Direct link to Terminal Applications")

Terminal editors use a custom `dank16` algorithm alongside matugen to generate a palette that honors the theme aesthetic while also providing 16 ansi colors.

### Ghostty[​](#ghostty "Direct link to Ghostty")

```
echo "config-file = ./config-dankcolors" >> ~/.config/ghostty/config
```

Optional - disable excessive notifications:

```
echo "app-notifications = no-clipboard-copy,no-config-reload" >> ~/.config/ghostty/config
```

### kitty[​](#kitty "Direct link to kitty")

```
echo "include dank-tabs.conf" >> ~/.config/kitty/kitty.conf  
echo "include dank-theme.conf" >> ~/.config/kitty/kitty.conf
```

### foot[​](#foot "Direct link to foot")

foot requires absolute paths in its configuration, edit `~/.config/foot/foot.ini` to add the include:

```
[main]  
include=/home/<USERNAME>/.config/foot/dank-colors.ini
```

### alacritty[​](#alacritty "Direct link to alacritty")

Add the alacritty theme to your imports secton in `~/.config/alacritty/alacritty.toml`

```
[general]  
import = [  
    "~/.config/alacritty/dank-theme.toml"  
]
```

Reload or restart the terminal to apply colors.

## Troubleshooting[​](#troubleshooting "Direct link to Troubleshooting")

**GTK apps not themed:**

* Verify `adw-gtk-theme` is installed
* Check that symlinks exist: `ls -la ~/.config/gtk-3.0/gtk.css`
* Ensure "Apply GTK Themes" is toggled in Settings

**Qt apps not themed:**

* Verify environment variables are set in compositor config
* Restart compositor session after changing environment
* Check `qt6ct` is installed if using Option 2
* Ensure "Apply Qt Themes" is toggled in Settings

**Firefox theme not working:**

* Verify `about:config` settings are correct
* Check that theme files exist in profile directory
* Try disabling other Firefox theme extensions
* Restart Firefox after making changes

**Terminal colors not updating:**

* Verify config lines are added to terminal config
* Check that theme files exist in `~/.config/DankMaterialShell/`
* Restart terminal application
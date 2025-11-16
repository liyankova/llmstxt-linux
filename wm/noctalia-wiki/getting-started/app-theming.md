---
source_url: "https://docs.noctalia.dev/getting-started/app-theming/"
title: "Basic App Theming | Noctalia Docs"
crawl_date: "2025-11-16T08:46:59.895550Z"
selector: "main"
---

# Basic App Theming | Noctalia Docs

# Basic App Theming

Noctalia includes powerful theming capabilities that can automatically apply your chosen color scheme to various applications. Whether you’re using colors from your wallpaper or a predefined scheme, Noctalia can keep your entire desktop consistent.

## Built-in Application Support

[Section titled “Built-in Application Support”](#built-in-application-support)

Noctalia comes with pre-configured templates for popular applications. Simply enable the ones you want to theme in **Settings → Color Scheme → Templates**.

### Supported Applications

[Section titled “Supported Applications”](#supported-applications)

#### Desktop Environments

[Section titled “Desktop Environments”](#desktop-environments)

* **GTK 3/4** - Themes all GTK-based applications (GNOME apps, many Linux applications)
* **Qt5ct/Qt6ct** - Themes Qt-based applications (KDE apps, many cross-platform apps)
* **KColorScheme** - Native KDE Plasma color scheme support

#### Terminals

[Section titled “Terminals”](#terminals)

* **Kitty** - Fast, GPU-accelerated terminal emulator
* **Foot** - Lightweight Wayland terminal
* **Ghostty** - Modern terminal emulator

#### Other Applications

[Section titled “Other Applications”](#other-applications)

* **Fuzzel** - Application launcher
* **Discord** - Discord clients like vesktop, equibop etc can all be themed
* **Firefox (via Pywalfox)** - Browser theming through the Pywalfox extension

## How to Enable Theming

[Section titled “How to Enable Theming”](#how-to-enable-theming)

#### General

[Section titled “General”](#general)

1. Open **Settings**
2. Navigate to **Color Scheme** tab
3. Scroll down to the **Templates** section
4. Toggle on the applications you want to theme
5. Your color scheme will be applied automatically

#### QT

[Section titled “QT”](#qt)

1. Install **`qt5ct`&`qt6ct`**
2. Set the environment variable **`QT_QPA_PLATFORMTHEME`** to `qt5ct` or `qt6ct`
3. Open **Settings**
4. Navigate to **Color Scheme** tab
5. Scroll down to the **Templates** section
6. Toggle on the **Qt**
7. Open **`qt5ct`** and **`qt6ct`**
8. Select `noctalia` in the **color scheme** and save
9. Your QT applications will applied the noctalia color scheme

#### GTK

[Section titled “GTK”](#gtk)

1. Install **`adw-gtk-theme`** & **`nwg-look(Optional)`**
2. If you installed `nwg-look`,just select `adw-gtk3` then apply
   ![nwg-look](/_astro/nwg-look.C2wKadob_ZzzNAo.webp)
3. You can also use the following command to set if you don’t want to install `nwg-look`

Terminal window

```
gsettings set org.gnome.desktop.interface gtk-theme 'adw-gtk3'
```

4. Open **Settings**
5. Navigate to **Color Scheme** tab
6. Scroll down to the **Templates** section
7. Toggle on the **GTK**
8. If some GTK applications is running, you may need to completely restart them for it to work
9. Your GTK applications will applied the noctalia color scheme

#### Discord

[Section titled “Discord”](#discord)

1. Noctalia supports `Vencord`, `Vesktop`, `Webcord`, `Armcord`, `Equibop`, `Lightcord`, and `Dorion`. Choose one or more of your preferred ones to install.
2. Open **Settings**
3. Navigate to **Color Scheme** tab
4. Scroll down to the **Templates** section
5. Toggle on the **Discord**
6. Open **Settings of Discord**
7. Select **Themes** then toggle on the **LunarCord(HyprLuna theme)**
   ![Discord](/_astro/discord.6vSQU6Co_JBubc.webp)
8. Your Discord will applied the noctalia color scheme

## Color Sources

[Section titled “Color Sources”](#color-sources)

Noctalia supports two ways to generate color schemes:

### Wallpaper Colors

[Section titled “Wallpaper Colors”](#wallpaper-colors)

When enabled, Noctalia uses **Matugen** to extract colors from your wallpaper and generate a Material You color scheme.

* Automatically updates when you change wallpapers
* Creates harmonious colors based on your wallpaper
* Requires `matugen` package

### Predefined Schemes

[Section titled “Predefined Schemes”](#predefined-schemes)

Choose from carefully crafted color schemes:

* **Noctalia (default)** - The original Noctalia color palette
* **Noctalia (legacy)** - Classic Noctalia colors
* **Tokyo Night** - Popular dark theme
  and many more!
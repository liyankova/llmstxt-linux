---
source_url: "https://danklinux.com/docs/dankmaterialshell/nixos"
title: "NixOS Installation | Dank Linux"
crawl_date: "2025-11-16T08:42:00.979343Z"
selector: "article"
---

# NixOS Installation | Dank Linux

* DankMaterialShell (dms)
* Installation - NixOS

On this page

```
██████╗ ███╗   ███╗███████╗
██╔══██╗████╗ ████║██╔════╝
██║  ██║██╔████╔██║███████╗
██║  ██║██║╚██╔╝██║╚════██║
██████╔╝██║ ╚═╝ ██║███████║
╚═════╝ ╚═╝     ╚═╝╚══════╝
```

DankMaterialShell can be installed on NixOS using home-manager with a declarative configuration. This guide covers the flake-based installation method.

## Installation via home-manager[​](#installation-via-home-manager "Direct link to Installation via home-manager")

### 1. Add Flake Inputs[​](#1-add-flake-inputs "Direct link to 1. Add Flake Inputs")

First, add the required flake inputs to your `flake.nix`:

```
{  
  inputs = {  
    nixpkgs.url = "github:NixOS/nixpkgs/nixos-unstable";  
  
    dgop = {  
      url = "github:AvengeMedia/dgop";  
      inputs.nixpkgs.follows = "nixpkgs";  
    };  
  
    dankMaterialShell = {  
      url = "github:AvengeMedia/DankMaterialShell";  
      inputs.nixpkgs.follows = "nixpkgs";  
      inputs.dgop.follows = "dgop";  
    };  
  };  
}
```

### 2. Import the Home Module[​](#2-import-the-home-module "Direct link to 2. Import the Home Module")

Add the DankMaterialShell home module to your home-manager imports:

```
imports = [  
  inputs.dankMaterialShell.homeModules.dankMaterialShell.default  
];
```

### 3. Enable DankMaterialShell[​](#3-enable-dankmaterialshell "Direct link to 3. Enable DankMaterialShell")

In your home-manager configuration, enable DankMaterialShell:

```
programs.dankMaterialShell.enable = true;
```

That's it! Rebuild your system and DankMaterialShell will be installed with sensible defaults.

## niri Integration[​](#niri-integration "Direct link to niri Integration")

If you're using the niri compositor, DankMaterialShell provides additional integration options including automatic keybindings and startup configuration.

### Prerequisites[​](#prerequisites "Direct link to Prerequisites")

First, ensure you have [niri-flake](https://github.com/sodiboo/niri-flake) in your inputs:

```
niri = {  
  url = "github:sodiboo/niri-flake";  
  inputs.nixpkgs.follows = "nixpkgs";  
};
```

Import it in your home-manager configuration:

```
imports = [  
  inputs.niri.homeModules.niri  
];
```

### Enable niri Module[​](#enable-niri-module "Direct link to Enable niri Module")

Now you can import and use the niri-specific DankMaterialShell module:

```
imports = [  
  inputs.dankMaterialShell.homeModules.dankMaterialShell.default  
  inputs.dankMaterialShell.homeModules.dankMaterialShell.niri  
];
```

Enable niri integration features:

```
programs.dankMaterialShell = {  
  enable = true;  
  niri = {  
    enableKeybinds = true;   # Automatic keybinding configuration  
    enableSpawn = true;      # Auto-start DMS with niri  
  };  
};
```

This will automatically configure keybindings for launcher, notifications, settings, and all other DankMaterialShell features.

## Configuration Options[​](#configuration-options "Direct link to Configuration Options")

DankMaterialShell provides numerous configuration options to customize your installation. Here are the main options:

### Feature Toggles[​](#feature-toggles "Direct link to Feature Toggles")

```
programs.dankMaterialShell = {  
  enable = true;  
  
  systemd = {  
    enable = true;             # Systemd service for auto-start  
    restartIfChanged = true;   # Auto-restart dms.service when dankMaterialShell changes  
  };  
    
  # Core features  
  enableSystemMonitoring = true;     # System monitoring widgets (dgop)  
  enableClipboard = true;            # Clipboard history manager  
  enableVPN = true;                  # VPN management widget  
  enableBrightnessControl = true;    # Backlight/brightness controls  
  enableColorPicker = true;          # Color picker tool  
  enableDynamicTheming = true;       # Wallpaper-based theming (matugen)  
  enableAudioWavelength = true;      # Audio visualizer (cava)  
  enableCalendarEvents = true;       # Calendar integration (khal)  
  enableSystemSound = true;          # System sound effects  
};
```

### Default Settings[​](#default-settings "Direct link to Default Settings")

You can pre-configure default settings that will be used on first launch:

```
programs.dankMaterialShell = {  
  enable = true;  
  
  default.settings = {  
    theme = "dark";  
    dynamicTheming = true;  
    # Add any other settings here  
  };  
  
  default.session = {  
    # Session state defaults  
  };  
};
```

These defaults are only applied if the settings files don't already exist, so they won't override your existing configuration.

### Custom Quickshell Package[​](#custom-quickshell-package "Direct link to Custom Quickshell Package")

If you need a specific version of Quickshell:

```
programs.dankMaterialShell = {  
  enable = true;  
  quickshell.package = pkgs.quickshell; # or your custom package  
};
```

### Plugins[​](#plugins "Direct link to Plugins")

Install DankMaterialShell plugins declaratively:

```
programs.dankMaterialShell = {  
  enable = true;  
  
  plugins = {  
    myPlugin = {  
      enable = true;  
      src = ./path/to/plugin;  
    };  
  };  
};
```

## Advanced Configuration[​](#advanced-configuration "Direct link to Advanced Configuration")

For a complete list of available options, check the module files:

* Base module: `distro/nix/default.nix` in the DankMaterialShell repository
* niri module: `distro/nix/niri.nix` in the DankMaterialShell repository

## Rebuilding[​](#rebuilding "Direct link to Rebuilding")

After making configuration changes, rebuild your system:

```
# For home-manager standalone  
home-manager switch  
  
# For NixOS with home-manager as a module  
sudo nixos-rebuild switch
```

## Troubleshooting[​](#troubleshooting "Direct link to Troubleshooting")

### DMS doesn't start automatically[​](#dms-doesnt-start-automatically "Direct link to DMS doesn't start automatically")

Make sure you have either:

* `systemd.enable = true` for systemd-based startup, or
* `niri.enableSpawn = true` for niri-managed startup

### Missing dependencies[​](#missing-dependencies "Direct link to Missing dependencies")

Each feature has its own dependency set. If a feature isn't working, ensure the corresponding `enable` option is set to `true`. For example, clipboard history requires `enableClipboard = true` which installs `cliphist` and `wl-clipboard`.

### Custom keybindings conflict with niri defaults[​](#custom-keybindings-conflict-with-niri-defaults "Direct link to Custom keybindings conflict with niri defaults")

If `niri.enableKeybinds = true` conflicts with your existing niri configuration, you can disable it and manually configure keybindings using the examples in the [Keybinds & IPC](/docs/dankmaterialshell/keybinds-ipc) guide.

## Next Steps[​](#next-steps "Direct link to Next Steps")

* Configure your preferences via [Themes](/docs/dankmaterialshell/application-themes)
* Set up compositor keybindings in [Keybinds & IPC](/docs/dankmaterialshell/keybinds-ipc)
* Extend functionality with [Plugins](/docs/dankmaterialshell/plugins-overview)
---
source_url: "https://danklinux.com/docs/dankgreeter/nixos"
title: "NixOS Installation | Dank Linux"
crawl_date: "2025-11-16T08:43:42.461201Z"
selector: "article"
---

# NixOS Installation | Dank Linux

* DankGreeter (dms-greeter)
* Installation - NixOS

On this page

```
██████╗  █████╗ ███╗   ██╗██╗  ██╗ ██████╗ ██████╗ ███████╗███████╗████████╗
██╔══██╗██╔══██╗████╗  ██║██║ ██╔╝██╔════╝ ██╔══██╗██╔════╝██╔════╝╚══██╔══╝
██║  ██║███████║██╔██╗ ██║█████╔╝ ██║  ███╗██████╔╝█████╗  █████╗     ██║
██║  ██║██╔══██║██║╚██╗██║██╔═██╗ ██║   ██║██╔══██╗██╔══╝  ██╔══╝     ██║
██████╔╝██║  ██║██║ ╚████║██║  ██╗╚██████╔╝██║  ██║███████╗███████╗   ██║
╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═══╝╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═╝╚══════╝╚══════╝   ╚═╝
```

DankGreeter can be installed on NixOS using the NixOS module. This guide covers the flake-based installation method.

## Installation[​](#installation "Direct link to Installation")

### 1. Add Flake Inputs[​](#1-add-flake-inputs "Direct link to 1. Add Flake Inputs")

Add the required flake inputs to your `flake.nix` if you haven't yet:

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

### 2. Import the NixOS Module[​](#2-import-the-nixos-module "Direct link to 2. Import the NixOS Module")

Add the DankGreeter module to your NixOS configuration imports:

```
imports = [  
  inputs.dankMaterialShell.nixosModules.greeter  
];
```

note

This import is of the NixOS module, rather than the home-manager module on the dms NixOS installation page.

### 3. Enable DankGreeter[​](#3-enable-dankgreeter "Direct link to 3. Enable DankGreeter")

Enable and configure the greeter:

```
programs.dankMaterialShell.greeter = {  
  enable = true;  
  compositor.name = "niri";  # Or "hyprland" or "sway"  
};
```

note

This is in your NixOS top-level configuration, not in the home-manager configuration like in the dms NixOS installation page.

## Configuration Options[​](#configuration-options "Direct link to Configuration Options")

```
programs.dankMaterialShell.greeter = {  
  compositor = {  
    name = "niri"; # Required. Can be also "hyprland" or "sway"  
    customConfig = ''  
      # Optional custom compositor configuration  
    '';  
  };  
  
  # Sync your user's DankMaterialShell theme with the greeter. You'll probably want this  
  configHome = "/home/yourusername";  
  
  # Custom config files for non-standard config locations  
  configFiles = [  
    "/home/yourusername/.config/DankMaterialShell/settings.json"  
  ];  
  
  # Save the logs to a file  
  logs = {  
    save = true;   
    path = "/tmp/dms-greeter.log";  
  };  
  
  # Custom Quickshell Package      
  quickshell.package = pkgs.quickshell;  
};
```

## Rebuilding[​](#rebuilding "Direct link to Rebuilding")

After making configuration changes, don't forget to rebuild your configuration:

```
sudo nixos-rebuild switch
```
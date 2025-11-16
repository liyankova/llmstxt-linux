---
source_url: "https://danklinux.com/docs/dgop/installation"
title: "Installation | Dank Linux"
crawl_date: "2025-11-16T08:43:53.440171Z"
selector: "article"
---

# Installation | Dank Linux

* DankGOP (dgop)
* Installation

On this page

```
██████╗  ██████╗  ██████╗ ██████╗
██╔══██╗██╔════╝ ██╔═══██╗██╔══██╗
██║  ██║██║  ███╗██║   ██║██████╔╝
██║  ██║██║   ██║██║   ██║██╔═══╝
██████╔╝╚██████╔╝╚██████╔╝██║
╚═════╝  ╚═════╝  ╚═════╝ ╚═╝
```

note

`dgop` has zero dependencies and compiles to a single static binary.

### Distribution Packages[​](#distribution-packages "Direct link to Distribution Packages")

#### Arch Linux[​](#arch-linux "Direct link to Arch Linux")

```
sudo pacman -S dgop
```

#### Fedora[​](#fedora "Direct link to Fedora")

```
sudo dnf copr enable avengemedia/danklinux  
sudo dnf install dgop
```

### Pre-built Binaries[​](#pre-built-binaries "Direct link to Pre-built Binaries")

Download the latest release for your architecture:

```
# Download and install  
wget https://github.com/AvengeMedia/dgop/releases/latest/download/dgop-linux-amd64.gz  
gunzip dgop-linux-amd64.gz  
chmod +x dgop-linux-amd64  
sudo mv dgop-linux-amd64 /usr/local/bin/dgop
```

### From Source[​](#from-source "Direct link to From Source")

Requirements: Go 1.24+

```
git clone https://github.com/AvengeMedia/dgop  
cd dgop  
make  
sudo make install
```

## Verification[​](#verification "Direct link to Verification")

Test the installation:

```
# Check version  
dgop version  
  
# Get system metrics  
dgop system  
  
# Run API server  
dgop server  
  
# See available commands  
dgop --help
```

## System Requirements[​](#system-requirements "Direct link to System Requirements")

* **Operating System**: Linux (uses `/proc` and `/sys` filesystems)
* **Go Version**: 1.24+ (for building from source)

### Optional Dependencies[​](#optional-dependencies "Direct link to Optional Dependencies")

For enhanced functionality:

* `nvidia-smi` - NVIDIA GPU monitoring

## Integration with DMS[​](#integration-with-dms "Direct link to Integration with DMS")

tip

DankMaterialShell users gain access to system widgets (CPU, RAM, GPU, Disk, Network) and process monitoring when dgop is installed.

## Next Steps[​](#next-steps "Direct link to Next Steps")

* [Configuration](/docs/dgop/configuration) - Configure dgop
* [Usage](/docs/dgop/usage) - Learn CLI commands and API usage
---
source_url: "https://danklinux.com/docs/danksearch/installation"
title: "Installation | Dank Linux"
crawl_date: "2025-11-16T08:44:17.287062Z"
selector: "article"
---

# Installation | Dank Linux

* DankSearch (dsearch)
* Installation

On this page

```
██████╗ ███████╗███████╗ █████╗ ██████╗  ██████╗██╗  ██╗
██╔══██╗██╔════╝██╔════╝██╔══██╗██╔══██╗██╔════╝██║  ██║
██║  ██║███████╗█████╗  ███████║██████╔╝██║     ███████║
██║  ██║╚════██║██╔══╝  ██╔══██║██╔══██╗██║     ██╔══██║
██████╔╝███████║███████╗██║  ██║██║  ██║╚██████╗██║  ██║
╚═════╝ ╚══════╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝ ╚═════╝╚═╝  ╚═╝
```

note

`dsearch` has zero dependencies and compiles to a single static binary.

### Distribution Packages[​](#distribution-packages "Direct link to Distribution Packages")

#### Arch Linux (AUR)[​](#arch-linux-aur "Direct link to Arch Linux (AUR)")

```
paru -S dsearch-bin  
  
# Development version  
paru -S dsearch-git
```

#### Fedora[​](#fedora "Direct link to Fedora")

```
sudo dnf copr enable avengemedia/danklinux  
sudo dnf install dsearch
```

### Pre-built Binaries[​](#pre-built-binaries "Direct link to Pre-built Binaries")

Download the latest release for your architecture:

```
# Download and install  
wget https://github.com/AvengeMedia/danksearch/releases/latest/download/dsearch-linux-amd64.gz  
gunzip dsearch-linux-amd64.gz  
chmod +x dsearch-linux-amd64  
sudo mv dsearch-linux-amd64 /usr/local/bin/dsearch
```

Install the systemd user unit and enable it.

```
wget https://raw.githubusercontent.com/AvengeMedia/danksearch/refs/heads/master/assets/dsearch.service  
mv dsearch.service ~/.config/systemd/user  
systemctl --user enable --now dsearch
```

### From Source[​](#from-source "Direct link to From Source")

Requirements: Go 1.24+

```
git clone https://github.com/AvengeMedia/danksearch  
cd danksearch  
make  
sudo make install  
make install-service
```

## Verification[​](#verification "Direct link to Verification")

Test the installation:

```
# Check version  
dsearch version  
  
# Build initial index  
dsearch index generate
```

## System Requirements[​](#system-requirements "Direct link to System Requirements")

* **Operating System**: Unix-based, compatible with most Unix-based operating systems (Linux, MacOS, BSD)
* **Go Version**: 1.24+ (for building from source)

## Integration with DMS[​](#integration-with-dms "Direct link to Integration with DMS")

tip

DankMaterialShell users can initiate filesystem search by typing `/` in the launcher when dsearch is installed.

## Next Steps[​](#next-steps "Direct link to Next Steps")

* [Configuration](/docs/danksearch/configuration) - Configure dsearch
* [Usage](/docs/danksearch/usage) - Learn CLI commands and API usage
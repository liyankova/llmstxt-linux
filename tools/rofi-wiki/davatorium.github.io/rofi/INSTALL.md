---
source_url: "https://davatorium.github.io/rofi/INSTALL/"
title: "Installation - Rofi Documentation"
crawl_date: "2025-11-16T15:10:47.718653Z"
selector: "article"
---

# Installation - Rofi Documentation

# Installation guide

This guide explains how to install rofi using its build system and how you can
make debug builds.

Rofi uses [Meson](https://mesonbuild.com/) as build system.
Be default rofi builds with both backends (x11 and wayland) if available on the
system. If no backend is found, it will give an error.
You can force the build system to disable the [wayland](#disable-wayland-support)
or [x11](#disable-x11-support) backend.

## DEPENDENCY

### For building

* C compiler that supports the c99 standard. (gcc or clang)
* meson
* ninja
* pkg-config
* flex 2.5.39 or higher
* bison
* check (Can be disabled using the `--disable-check` configure flag)
  check is used for build-time tests and does not affect functionality.
* Developer packages of the external libraries
* glib-compile-resources

### External libraries

* libpango >= 1.50
* libpangocairo
* libcairo
* libcairo-xcb
* libglib2.0 >= 2.72
* gmodule-2.0
* gio-unix-2.0
* libgdk-pixbuf-2.0
* libstartup-notification-1.0
* libxkbcommon >= 0.4.1
* libxkbcommon-x11
* libxcb (sometimes split, you need libxcb, libxcb-xkb and libxcb-randr
  libxcb-xinerama)
* xcb-util
* xcb-util-wm (sometimes split as libxcb-ewmh and libxcb-icccm)
* xcb-util-cursor
* xcb-imdkit (optional, 1.0.3 or up preferred)

On debian based systems, the developer packages are in the form of:
`<package>-dev` on rpm based `<package>-devel`.

For wayland support:

* wayland
* wayland-protocols >= 1.17

## Install from a release

When downloading from the github release page, make sure to grab the archive
`rofi-{version}.tar.[g|x]z`. The auto-attached files `source code (zip|tar.gz)`
by github do not contain a valid release. It misses a setup build system and
includes irrelevant files.

### Meson

Check dependencies and configure build system:

```
    meson setup build
```

Build Rofi:

```
    ninja -C build
```

The actual install, execute as root (if needed):

```
    ninja -C build install
```

The default installation prefix is: `/usr/local/` use `meson setup build
--prefix={prefix}` to install into another location.

## Install a checkout from git

The GitHub Pages version of these directions may be out of date. Please use
[INSTALL.md from the online repo](https://github.com/DaveDavenport/rofi/blob/master/INSTALL.md#install-a-checkout-from-git) or your local repository.

If you don't have a checkout:

```
    git clone --recursive https://github.com/DaveDavenport/rofi
    cd rofi/
```

If you already have a checkout:

```
    cd rofi/
    git pull
    git submodule update --init
```

From this point, use the same steps you use for a release.

## Options for building

When you run the configure step there are several options you can configure.

For Meson, before the initial setup, you can see rofi options in
`meson_options.txt` and Meson options with `meson setup --help`. Meson's
built-in options can be set using regular command line arguments, like so:
`meson setup build --option=value`. Rofi-specific options can be set using the
`-D` argument, like so: `meson setup build -Doption=value`. After the build dir
is set up by `meson setup build`, the `meson configure build` command can be
used to configure options, by the same means.

The most useful one to set is the installation prefix:

```
    # Meson
    meson setup build --prefix <installation path>
```

f.e.

```
    # Meson
    meson setup build --prefix /usr
```

### Disable x11 support

```
meson setup build -Dxcb=disabled
```

### Disable wayland support

```
meson setup build -Dwayland=disabled
```

### Install locally

or to install locally:

```
    # Meson
    meson setup build --prefix ${HOME}/.local
```

### Verbose build output

Show the commands called (when using ninja):

```
    # Meson
    ninja -C build -v
```

### Debug build

Compile with debug symbols and no optimization, this is useful for making
backtraces:

```
    # Meson
    meson configure build --debug
    ninja -C build
```

### Get a backtrace

Getting a backtrace using GDB is not very handy. Because if rofi get stuck, it
grabs keyboard and mouse. So if it crashes in GDB you are stuck. The best way
to go is to enable core file. (ulimit -c unlimited in bash) then make rofi
crash. You can then load the core in GDB.

```
    # Meson (because it uses a separate build directory)
    gdb build/rofi core
```

> Where the core file is located and what its exact name is different on each
> distributions. Please consult the relevant documentation.

For more information see the rofi-debugging(5) manpage.

## Install distribution

### Debian or Ubuntu

```
    apt install rofi
```

### Fedora

```
    dnf install rofi
```

### ArchLinux

```
    pacman -S rofi
```

### Gentoo

An ebuild is available, `x11-misc/rofi`. It's up to date, but you may need to
enable ~arch to get the latest release:

```
    echo 'x11-misc/rofi ~amd64' >> /etc/portage/package.accept_keywords
```

for amd64 or:

```
    echo 'x11-misc/rofi ~x86' >> /etc/portage/package.accept_keywords
```

for i386.

To install it, simply issue `emerge rofi`.

### openSUSE

On both openSUSE Leap and openSUSE Tumbleweed rofi can be installed using:

```
    sudo zypper install rofi
```

### FreeBSD

```
    sudo pkg install rofi
```

### macOS

On macOS rofi can be installed via [MacPorts](https://www.macports.org):

```
    sudo port install rofi
```
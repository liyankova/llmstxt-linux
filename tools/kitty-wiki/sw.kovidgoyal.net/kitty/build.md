---
source_url: "https://sw.kovidgoyal.net/kitty/build/"
title: "Build from source - kitty"
crawl_date: "2025-11-16T14:47:54.851274Z"
selector: "article"
---

# Build from source - kitty

# Build from source[¶](#build-from-source "Link to this heading")

[![Build status](https://github.com/kovidgoyal/kitty/workflows/CI/badge.svg)](https://github.com/kovidgoyal/kitty/actions?query=workflow%3ACI)

Note

If you just want to test the latest changes to kitty, you don’t need to build
from source. Instead install the [latest nightly build](../binary/#nightly).

*kitty* is designed to run from source, for easy hack-ability. All you need to
get started is a C compiler and the [go compiler](https://go.dev/doc/install) (on Linux, the [X11 development libraries](#x11-dev-libs) as well).
After installing those, run the following commands:

```
git clone https://github.com/kovidgoyal/kitty.git && cd kitty
./dev.sh build
```

That’s it, kitty will be built from source, magically. You can run it as
`kitty/launcher/kitty`.

This works, because the `./dev.sh build` command downloads all the major
dependencies of kitty as pre-built binaries for your platform and builds kitty
to use these rather than system libraries. The few required system libraries
are X11 and DBUS on Linux.

If you make changes to kitty code, simply re-run `./dev.sh build`
to build kitty with your changes.

Note

If you plan to run kitty from source long-term, there are a couple of
caveats to be aware of. You should occasionally run `./dev.sh deps`
to have the dependencies re-downloaded as they are updated periodically.
Also, the built kitty executable assumes it will find source in whatever
directory you first ran `./dev.sh build` in. If you move/rename the
directory, run `make clean && ./dev.sh build`. You should also create
symlinks to the `kitty` and `kitten` binaries from somewhere
in your PATH so that they can be conveniently launched.

Note

On macOS, you can use `kitty/launcher/kitty.app` to run kitty as well,
but note that this is an unsigned kitty.app so some functionality such as
notifications will not work as Apple disallows this. If you need this
functionality, you can try signing the built `kitty.app` with a self
signed certificate, see for example, [here](https://stackoverflow.com/questions/27474751/how-can-i-codesign-an-app-without-being-in-the-mac-developer-program/27474942).

## Building in debug mode[¶](#building-in-debug-mode "Link to this heading")

The following will build with debug symbols:

```
./dev.sh build --debug
```

To build with sanitizers and debug symbols:

```
./dev.sh build --debug --sanitize
```

For more help on the various options supported by the build script:

```
./dev.sh build -h
```

### Building the documentation[¶](#building-the-documentation "Link to this heading")

To have the kitty documentation available locally, run:

```
./dev.sh deps -for-docs && ./dev.sh docs
```

To develop the docs, with live reloading, use:

```
./dev.sh deps -for-docs && ./dev.sh docs -live-reload
```

### Dependencies[¶](#dependencies "Link to this heading")

These dependencies are needed when building against system libraries only.

Run-time dependencies:

* `python` >= 3.8
* `harfbuzz` >= 2.2.0
* `zlib`
* `libpng`
* `liblcms2`
* `libxxhash`
* `openssl`
* `pixman` (not needed on macOS)
* `cairo` (not needed on macOS)
* `freetype` (not needed on macOS)
* `fontconfig` (not needed on macOS)
* `libcanberra` (not needed on macOS)
* `libsystemd` (optional, not needed on non systemd systems)
* `ImageMagick` (optional, needed to display uncommon image formats in the terminal)

Build-time dependencies:

* `gcc` or `clang`
* `simde`
* `go` >= 1.24.0 (see `go.mod` for go packages used during building)
* `pkg-config`
* Symbols NERD Font Mono either installed system-wide or placed in `fonts/SymbolsNerdFontMono-Regular.ttf`
* For building on Linux in addition to the above dependencies you might also
  need to install the following packages, if they are not already installed by
  your distro:

  + `liblcms2-dev`
  + `libfontconfig-dev`
  + `libssl-dev`
  + `libpython3-dev`
  + `libxxhash-dev`
  + `libsimde-dev`
  + `libcairo2-dev`

  Also, the X11 development libraries:

  + `libdbus-1-dev`
  + `libxcursor-dev`
  + `libxrandr-dev`
  + `libxi-dev`
  + `libxinerama-dev`
  + `libgl1-mesa-dev`
  + `libxkbcommon-x11-dev`
  + `libfontconfig-dev`
  + `libx11-xcb-dev`

### Build and run from source with Nix[¶](#build-and-run-from-source-with-nix "Link to this heading")

On NixOS or any other Linux or macOS system with the Nix package manager
installed, execute [nix-shell](https://nixos.org/guides/nix-pills/developing-with-nix-shell.html) to create
the correct environment to build kitty or use `nix-shell --pure` instead to
eliminate most of the influence of the outside system, e.g. globally installed
packages. `nix-shell` will automatically fetch all required dependencies and
make them available in the newly spawned shell.

Then proceed with `make` or `make app` according to the platform specific
instructions above.

### Notes for Linux/macOS packagers[¶](#notes-for-linux-macos-packagers "Link to this heading")

The released *kitty* source code is available as a [tarball](https://github.com/kovidgoyal/kitty/releases/download/v0.44.0/kitty-0.44.0.tar.xz) from
[the GitHub releases page](https://github.com/kovidgoyal/kitty/releases).

While *kitty* does use Python, it is not a traditional Python package, so please
do not install it in site-packages.
Instead run:

```
make linux-package
```

This will install *kitty* into the directory `linux-package`. You can run
*kitty* with `linux-package/bin/kitty`. All the files needed to run kitty
will be in `linux-package/lib/kitty`. The terminfo file will be installed
into `linux-package/share/terminfo`. Simply copy these files into
`/usr` to install *kitty*. In other words, `linux-package` is the
staging area into which *kitty* is installed. You can choose a different staging
area, by passing the `--prefix` argument to `setup.py`.

You should probably split *kitty* into three packages:

`kitty-terminfo`
:   Installs the terminfo file

`kitty-shell-integration`
:   Installs the shell integration scripts (the contents of the
    shell-integration directory in the kitty source code), probably to
    `/usr/share/kitty/shell-integration`

`kitty`
:   Installs the main program

This allows users to install the terminfo and shell integration files on
servers into which they ssh, without needing to install all of *kitty*. The
shell integration files **must** still be present in
`lib/kitty/shell-integration` when installing the kitty main package as
the kitty program expects to find them there.

Note

You need a couple of extra dependencies to build linux-package. `tic`
to compile terminfo files, usually found in the development package of
`ncurses`. Also, if you are building from a git checkout instead of the
released source code tarball, you will need to install the dependencies from
`docs/requirements.txt` to build the kitty documentation. They can be
installed most easily with `python -m pip -r docs/requirements.txt`.

This applies to creating packages for *kitty* for macOS package managers such as
Homebrew or MacPorts as well.

### Cross compilation[¶](#cross-compilation "Link to this heading")

While cross compilation is neither officially supported, nor recommended, as it
means the test suite cannot be run for the cross compiled build, there is some
support for cross compilation. Basically, run:

```
make prepare-for-cross-compile
```

Then setup the cross compile environment (CC, CFLAGS, PATH, etc.) and run:

```
make cross-compile
```

This will create the cross compiled build in the `linux-package`
directory.
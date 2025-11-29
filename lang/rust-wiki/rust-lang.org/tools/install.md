---
source_url: "https://rust-lang.org/tools/install"
title: "Install Rust - Rust Programming Language"
crawl_date: "2025-11-29T16:22:00.255049Z"
selector: "main"
---

# Install Rust - Rust Programming Language

It looks like you’re running macOS, Linux, or another Unix-like OS. To download Rustup and install Rust, run the following in your terminal, then follow the on-screen instructions. See ["Other Installation Methods"](https://forge.rust-lang.org/infra/other-installation-methods.html) if you are on Windows.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

It looks like you’re running Windows. To start using Rust, download the installer, then run the program and follow the onscreen instructions. You may need to install the [Visual Studio C++ Build tools](https://rust-lang.github.io/rustup/installation/windows-msvc.html) when prompted to do so. If you are not on Windows see ["Other Installation Methods"](https://forge.rust-lang.org/infra/other-installation-methods.html).

[Download rustup-init.exe (32-bit)](https://static.rust-lang.org/rustup/dist/i686-pc-windows-msvc/rustup-init.exe)

[Download rustup-init.exe (x64)](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe)

[Download rustup-init.exe (ARM64)](https://static.rust-lang.org/rustup/dist/aarch64-pc-windows-msvc/rustup-init.exe)

### Windows Subsystem for Linux

If you’re a Windows Subsystem for Linux user run the following in your terminal, then follow the on-screen instructions to install Rust.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

To install Rust, if you are running a Unix such as WSL, Linux or macOS,  
 run the following in your terminal, then follow the on-screen instructions.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

---

If you are running Windows,  
download and run [rustup‑init.exe](https://win.rustup.rs) then follow the on-screen instructions.

### Getting started

If you're just getting started with
Rust and would like a more detailed walk-through, see our
[getting started](            /learn/get-started
) page.

### Windows considerations

On Windows, Rust additionally requires the MSVC build tools
for Visual Studio 2013 or later. See
[MSVC prerequistes](https://rust-lang.github.io/rustup/installation/windows-msvc.html)

For further information about configuring Rust on Windows see the
[Windows-specific `rustup` documentation](https://rust-lang.github.io/rustup/installation/windows.html).

### Toolchain management with `rustup`

Rust is installed and managed by the
[`rustup`](https://rust-lang.github.io/rustup/)
tool. Rust has a 6-week
[rapid release process](https://github.com/rust-lang/rfcs/blob/master/text/0507-release-channels.md) and supports a
[great
number of platforms](https://forge.rust-lang.org/release/platform-support.html), so there are many builds of Rust available at
any time. `rustup` manages these builds in a consistent way
on every platform that Rust supports, enabling installation of Rust
from the beta and nightly release channels as well as support for
additional cross-compilation targets.

If you've installed `rustup` in the past, you can update
your installation by running `rustup update`.

For more information see the
[`rustup` documentation](https://rust-lang.github.io/rustup/).

### Configuring the `PATH` environment variable

In the Rust development environment, all tools are installed to the
`~/.cargo/bin`

`%USERPROFILE%\.cargo\bin`
 directory, and this is where you will find the Rust toolchain,
including `rustc`, `cargo`, and `rustup`.

Accordingly, it is customary for Rust developers to include this
directory in their
[`PATH` environment variable](https://en.wikipedia.org/wiki/PATH_(variable)). During installation
`rustup` will attempt to configure the `PATH`.
Because of differences between platforms, command shells, and bugs in
`rustup`, the modifications to `PATH` may not
take effect until the console is restarted, or the user is logged out,
or it may not succeed at all.

If, after installation, running `rustc --version` in the
console fails, this is the most likely reason.

### Uninstall Rust

If at any point you would like to uninstall Rust, you can run
`rustup self uninstall`.
We'll miss you though!

The installation described above, via
`rustup`, is the preferred way to install Rust for most
developers. However, Rust can be installed via other methods as well.

[Learn more](https://forge.rust-lang.org/infra/other-installation-methods.html)
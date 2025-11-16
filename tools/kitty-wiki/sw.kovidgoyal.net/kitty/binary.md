---
source_url: "https://sw.kovidgoyal.net/kitty/binary/"
title: "Install kitty - kitty"
crawl_date: "2025-11-16T14:47:52.680867Z"
selector: "article"
---

# Install kitty - kitty

# Install kitty[¶](#install-kitty "Link to this heading")

## Binary install[¶](#binary-install "Link to this heading")

You can install pre-built binaries of *kitty* if you are on macOS or Linux using
the following simple command:

```
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
```

The binaries will be installed in the standard location for your OS,
`/Applications/kitty.app` on macOS and `~/.local/kitty.app` on
Linux. The installer only touches files in that directory. To update kitty,
simply re-run the command.

Warning

**Do not** copy the kitty binary out of the installation folder. If you want
to add it to your [`PATH`](../glossary/#envvar-PATH), create a symlink in `~/.local/bin` or
`/usr/bin` or wherever. You should create a symlink for the `kitten`
binary as well. Whichever folder you choose to create the symlink in should
be in the **systemwide** PATH, a folder added to the PATH in your shell rc
files will not work when running kitty from your desktop environment.

## Manually installing[¶](#manually-installing "Link to this heading")

If something goes wrong or you simply do not want to run the installer, you can
manually download and install *kitty* from the [GitHub releases page](https://github.com/kovidgoyal/kitty/releases). If you are on macOS, download
the `.dmg` and install as normal. If you are on Linux, download the
tarball and extract it into a directory. The *kitty* executable will be in the
`bin` sub-directory.

## Desktop integration on Linux[¶](#desktop-integration-on-linux "Link to this heading")

If you want the kitty icon to appear in the taskbar and an entry for it to be
present in the menus, you will need to install the `kitty.desktop` file.
The details of the following procedure may need to be adjusted for your
particular desktop, but it should work for most major desktop environments.

```
# Create symbolic links to add kitty and kitten to PATH (assuming ~/.local/bin is in
# your system-wide PATH)
ln -sf ~/.local/kitty.app/bin/kitty ~/.local/kitty.app/bin/kitten ~/.local/bin/
# Place the kitty.desktop file somewhere it can be found by the OS
cp ~/.local/kitty.app/share/applications/kitty.desktop ~/.local/share/applications/
# If you want to open text files and images in kitty via your file manager also add the kitty-open.desktop file
cp ~/.local/kitty.app/share/applications/kitty-open.desktop ~/.local/share/applications/
# Update the paths to the kitty and its icon in the kitty desktop file(s)
sed -i "s|Icon=kitty|Icon=$(readlink -f ~)/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g" ~/.local/share/applications/kitty*.desktop
sed -i "s|Exec=kitty|Exec=$(readlink -f ~)/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty*.desktop
# Make xdg-terminal-exec (and hence desktop environments that support it use kitty)
echo 'kitty.desktop' > ~/.config/xdg-terminals.list
```

Note

In `kitty-open.desktop`, kitty is registered to handle some supported
MIME types. This will cause kitty to take precedence on some systems where
the default apps are not explicitly set. For example, if you expect to use
other GUI file managers to open dir paths when using commands such as
**xdg-open**, you should configure the default opener for the MIME
type `inode/directory`:

```
xdg-mime default org.kde.dolphin.desktop inode/directory
```

Note

If you use the venerable [stow](https://www.gnu.org/software/stow/)
command to manage your manual installations, the following takes care of the
above for you (use with `dest=~/.local/stow`):

```
cd ~/.local/stow
stow -v kitty.app
```

## Customizing the installation[¶](#customizing-the-installation "Link to this heading")

* You can install the latest nightly kitty build with `installer`:

  ```
  curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin \
      installer=nightly
  ```

  If you want to install it in parallel to the released kitty specify a
  different install locations with `dest`:

  ```
  curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin \
      installer=nightly dest=/some/other/location
  ```
* You can specify a specific version to install, with:

  ```
  curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin \
      installer=version-0.35.2
  ```
* You can tell the installer not to launch *kitty* after installing it with
  `launch=n`:

  ```
  curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin \
      launch=n
  ```
* You can use a previously downloaded dmg/tarball, with `installer`:

  ```
  curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin \
      installer=/path/to/dmg or tarball
  ```

## Uninstalling[¶](#uninstalling "Link to this heading")

All the installer does is copy the kitty files into the install directory. To
uninstall, simply delete that directory.

## Building from source[¶](#building-from-source "Link to this heading")

*kitty* is easy to build from source, follow the [instructions](../build/).
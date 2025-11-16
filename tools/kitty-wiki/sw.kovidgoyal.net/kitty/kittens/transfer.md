---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/transfer/"
title: "Transfer files - kitty"
crawl_date: "2025-11-16T14:48:36.749549Z"
selector: "article"
---

# Transfer files - kitty

# Transfer files[¶](#transfer-files "Link to this heading")

Added in version 0.30.0.

Transfer files to and from remote computers over the `TTY` device itself.
This means that file transfer works over nested SSH sessions, serial links,
etc. Anywhere you have a terminal device, you can transfer files.

![The transfer kitten at work](../../_images/transfer.png)

This kitten supports transferring entire directory trees, preserving soft and
hard links, file permissions, times, etc. It even supports the [rsync](https://en.wikipedia.org/wiki/Rsync) protocol
to transfer only changes to large files.

See also

See the [Remote files](../remote_file/) kitten

## Basic usage[¶](#basic-usage "Link to this heading")

Simply ssh into a remote computer using the [ssh kitten](../ssh/) and run the this kitten
(which the ssh kitten makes available for you on the remote computer
automatically). Some illustrative examples are below. To copy a file from a
remote computer:

```
<local computer>  $ kitten ssh my-remote-computer
<remote computer> $ kitten transfer some-file /path/on/local/computer
```

This, will copy `some-file` from the computer into which you have SSHed
to your local computer at `/path/on/local/computer`. kitty will ask you
for confirmation before allowing the transfer, so that the file transfer
protocol cannot be abused to read/write files on your computer.

To copy a file from your local computer to the remote computer:

```
<local computer>  $ kitten ssh my-remote-computer
<remote computer> $ kitten transfer --direction=upload /path/on/local/computer remote-file
```

For more detailed usage examples, see the command line interface section below.

Note

If you dont want to use the ssh kitten, you can install the kitten binary on
the remote machine yourself, it is a standalone, statically compiled binary
available from the [kitty releases page](https://github.com/kovidgoyal/kitty/releases). Or you can write your own
script/program to use the underlying [file transfer protocol](../../file-transfer-protocol/).

## Avoiding the confirmation prompt[¶](#avoiding-the-confirmation-prompt "Link to this heading")

Normally, when you start a file transfer kitty will prompt you for confirmation.
This is to ensure that hostile programs running on a remote machine cannot
read/write files on your computer without your permission. If the remote machine
is trusted, then you can disable the confirmation prompt by:

1. Setting the [`file_transfer_confirmation_bypass`](../../conf/#opt-kitty.file_transfer_confirmation_bypass) option to some password.
2. When invoking the kitten use the [`--permissions-bypass`](#cmdoption-kitty-kitten-transfer-permissions-bypass) to supply the password you set
   in step one.

Warning

Using a password to bypass confirmation means any software running
on the remote machine could potentially learn that password and use it to
gain full access to your computer.

## Delta transfers[¶](#delta-transfers "Link to this heading")

This kitten has the ability to use the [rsync](https://en.wikipedia.org/wiki/Rsync) protocol to only transfer the
differences between files. To turn it on use the [`--transmit-deltas`](#cmdoption-kitty-kitten-transfer-transmit-deltas) option. Note that this will
actually be slower when transferring small files or on a very fast network, because
of round trip overhead, so use with care.

## Source code for transfer[¶](#source-code-for-transfer "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/transfer).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten transfer [options] source_files_or_directories destination_path
```

Transfer files over the TTY device. Can be used to send files between any two
computers provided there is a TTY connection between them, such as over SSH.
Supports copying files, directories (recursively), symlinks and hardlinks. Can
even use an rsync like protocol to copy only changes between files. When
copying multiple files, use the --confirm-paths option to see what exactly will
be copied. The easiest way to use this kitten is to first ssh into the remote
computer with the ssh kitten:

```
$ kitten ssh my-remote-computer
```

Then, on the remote computer run the transfer kitten to do your copying.
To copy a file from the remote computer to the local computer, run:

```
$ kitten transfer remote-file /path/to/local-file
```

This will copy `remote-file` from the remote computer to `/path/to/local-file`
on the local computer.

Similarly, to copy a file from the local computer to the remote one, run:

```
$ kitten transfer --direction=upload /path/to/local-file remote-file
```

This will copy `/path/to/local-file` from the local computer
to `remote-file` on the remote computer.

Multiple files can be copied:

```
$ kitten transfer file1 file2 /path/to/dir/
```

This will put `file1` and `file2` into the directory
`/path/to/dir/` on the local computer.

Directories can also be copied, recursively:

```
$ kitten transfer dir1 /path/to/dir/
```

This will put `dir1` and all its contents into
`/path/to/dir/` on the local computer.

Note that when copying multiple files or directories, the destination
must be an existing directory on the receiving computer. Relative file
paths are resolved with respect to the current directory on the computer
running the kitten and the home directory on the other computer. It is
a good idea to use the [`--confirm-paths`](#cmdoption-kitty-kitten-transfer-confirm-paths) command line flag to verify
the kitten will copy the files you expect it to.

### Options[¶](#options "Link to this heading")

--direction <DIRECTION>, -d <DIRECTION>[¶](#cmdoption-kitty-kitten-transfer-direction "Link to this definition")
:   Whether to send or receive files. `send` or `download` copy files from the computer on which the kitten is running (usually the remote computer) to the local computer. `receive` or `upload` copy files from the local computer to the remote computer.
    Default: `download`
    Choices: `download`, `receive`, `send`, `upload`

--mode <MODE>, -m <MODE>[¶](#cmdoption-kitty-kitten-transfer-mode "Link to this definition")
:   How to interpret command line arguments. In `mirror` mode all arguments are assumed to be files/dirs on the sending computer and they are mirrored onto the receiving computer. Files under the HOME directory are copied to the HOME directory on the receiving computer even if the HOME directory is different. In `normal` mode the last argument is assumed to be a destination path on the receiving computer. The last argument must be an existing directory unless copying a single file. When it is a directory it should end with a trailing slash.
    Default: `normal`
    Choices: `mirror`, `normal`

--compress <COMPRESS>[¶](#cmdoption-kitty-kitten-transfer-compress "Link to this definition")
:   Whether to compress data being sent. By default compression is enabled based on the type of file being sent. For files recognized as being already compressed, compression is turned off as it just wastes CPU cycles.
    Default: `auto`
    Choices: `always`, `auto`, `never`

--permissions-bypass <PERMISSIONS\_BYPASS>, -p <PERMISSIONS\_BYPASS>[¶](#cmdoption-kitty-kitten-transfer-permissions-bypass "Link to this definition")
:   The password to use to skip the transfer confirmation popup in kitty. Must match the password set for the [`file_transfer_confirmation_bypass`](../../conf/#opt-kitty.file_transfer_confirmation_bypass) option in `kitty.conf`. Note that leading and trailing whitespace is removed from the password. A password starting with `.`, `/` or `~` characters is assumed to be a file name to read the password from. A value of `-` means read the password from STDIN. A password that is purely a number less than 256 is assumed to be the number of a file descriptor from which to read the actual password.

--confirm-paths [=no], -c [=no][¶](#cmdoption-kitty-kitten-transfer-confirm-paths "Link to this definition")
:   Before actually transferring files, show a mapping of local file names to remote file names and ask for confirmation.

--transmit-deltas [=no], -x [=no][¶](#cmdoption-kitty-kitten-transfer-transmit-deltas "Link to this definition")
:   If a file on the receiving side already exists, use the rsync algorithm to update it to match the file on the sending side, potentially saving lots of bandwidth and also automatically resuming partial transfers. Note that this will actually degrade performance on fast links or with small files, so use with care.
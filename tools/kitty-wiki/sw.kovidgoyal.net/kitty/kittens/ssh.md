---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/ssh/"
title: "Truly convenient SSH - kitty"
crawl_date: "2025-11-16T14:48:39.041853Z"
selector: "article"
---

# Truly convenient SSH - kitty

# Truly convenient SSH[¶](#truly-convenient-ssh "Link to this heading")

* Automatic [Shell integration](../../shell-integration/#shell-integration) on remote hosts
* Easily [clone local shell/editor config](#real-world-ssh-kitten-config) on remote hosts
* Automatic [`re-use of existing connections`](#opt-kitten-ssh.share_connections) to avoid connection setup latency
* Make the kitten binary available in the remote host [`on demand`](#opt-kitten-ssh.remote_kitty)
* Easily [`change terminal colors`](#opt-kitten-ssh.color_scheme) when connecting to remote hosts
* Automatically [`forward the kitty remote control socket`](#opt-kitten-ssh.forward_remote_control) to configured hosts

Added in version 0.25.0: Automatic shell integration, file transfer and reuse of connections

Added in version 0.30.0: Automatic forwarding of remote control sockets

The ssh kitten allows you to login easily to remote hosts, and automatically
setup the environment there to be as comfortable as your local shell. You can
specify environment variables to set on the remote host and files to copy there,
making your remote experience just like your local shell. Additionally, it
automatically sets up [Shell integration](../../shell-integration/#shell-integration) on the remote host and copies the
kitty terminfo database there.

The ssh kitten is a thin wrapper around the traditional [ssh](https://man.openbsd.org/ssh)
command line program and supports all the same options and arguments and configuration.
In interactive usage scenarios it is a drop in replacement for **ssh**.
To try it out, simply run:

```
kitten ssh some-hostname-to-connect-to
```

You should end up at a shell prompt on the remote host, with shell integration
enabled. If you like it you can add an alias to it in your shell’s rc files:

```
alias s="kitten ssh"
```

So now you can just type `s hostname` to connect.

If you define a mapping in `kitty.conf` such as:

```
map f1 new_window_with_cwd
```

Then, pressing `F1` will open a new window automatically logged into the
same host using the ssh kitten, at the same directory.

The ssh kitten can be configured using the `~/.config/kitty/ssh.conf` file
where you can specify environment variables to set on the remote host and files
to copy from the local to the remote host. Let’s see a quick example:

```
# Copy the files and directories needed to setup some common tools
copy .zshrc .vimrc .vim
# Setup some environment variables
env SOME_VAR=x
# COPIED_VAR will have the same value on the remote host as it does locally
env COPIED_VAR=_kitty_copy_env_var_

# Create some per hostname settings
hostname someserver-*
copy env-files
env SOMETHING=else

hostname someuser@somehost
copy --dest=foo/bar some-file
copy --glob some/files.*
```

See below for full details on the syntax and options of `ssh.conf`.
Additionally, you can pass config options on the command line:

```
kitten ssh --kitten interpreter=python servername
```

The `--kitten` argument can be specified multiple times, with directives
from `ssh.conf`. These override the final options used for the matched host, as if they
had been appended to the end of the matching section for that host in
`ssh.conf`. They apply only to the host being SSHed to by this invocation,
so any [`hostname`](#opt-kitten-ssh.hostname) directives are ignored.

Warning

Due to limitations in the design of SSH, any typing you do before the
shell prompt appears may be lost. So ideally don’t start typing till you see
the shell prompt. 😇

## A real world example[¶](#a-real-world-example "Link to this heading")

Suppose you often SSH into a production server, and you would like to setup
your shell and editor there using your custom settings. However, other people
could SSH in as well and you don’t want to clobber their settings. Here is how
this could be achieved using the ssh kitten with **zsh** and
**vim** as the shell and editor, respectively:

```
# Have these settings apply to servers in my organization
hostname myserver-*

# Setup zsh to read its files from my-conf/zsh
env ZDOTDIR=$HOME/my-conf/zsh
copy --dest my-conf/zsh/.zshrc .zshrc
copy --dest my-conf/zsh/.zshenv .zshenv
# If you use other zsh init files add them in a similar manner

# Setup vim to read its config from my-conf/vim
env VIMINIT=$HOME/my-conf/vim/vimrc
env VIMRUNTIME=$HOME/my-conf/vim
copy --dest my-conf/vim .vim
copy --dest my-conf/vim/vimrc .vimrc
```

## How it works[¶](#how-it-works "Link to this heading")

The ssh kitten works by having SSH transmit and execute a POSIX sh (or
[`optionally`](#opt-kitten-ssh.interpreter) Python) bootstrap script on the
remote host using an [`interpreter`](#opt-kitten-ssh.interpreter). This script
reads setup data over the TTY device, which kitty sends as a Base64 encoded
compressed tarball. The script extracts it and places the [`files`](#opt-kitten-ssh.copy)
and sets the [`environment variables`](#opt-kitten-ssh.env) before finally
launching the [`login shell`](#opt-kitten-ssh.login_shell) with [`shell
integration`](#opt-kitten-ssh.shell_integration) enabled. The data is requested by
the kitten over the TTY with a random one time password. kitty reads the request
and if the password matches a password pre-stored in shared memory on the
localhost by the kitten, the transmission is allowed. If your local
[OpenSSH](https://www.openssh.com/) version is >= 8.4 then the data is
transmitted instantly without any roundtrip delay.

Note

When connecting to BSD hosts, it is possible the bootstrap script will fail
or run slowly, because the default shells are crippled in various ways.
Your best bet is to install Python on the remote, make sure the login shell
is something POSIX sh compliant, and use `python` as the
[`interpreter`](#opt-kitten-ssh.interpreter) in `ssh.conf`.

Note

This may or may not work when using terminal multiplexers, depending on
whether they passthrough the escape codes and if the values of the
environment variables [`KITTY_PID`](../../glossary/#envvar-KITTY_PID) and [`KITTY_WINDOW_ID`](../../glossary/#envvar-KITTY_WINDOW_ID) are
correct in the current session (they can be wrong when connecting to a tmux
session running in a different window) and the ssh kitten is run in the
currently active multiplexer window.

## Host bootstrap configuration[¶](#host-bootstrap-configuration "Link to this heading")

hostname[¶](#opt-kitten-ssh.hostname "Link to this definition")

```
hostname *
```

The hostname that the following options apply to. A glob pattern to match
multiple hosts can be used. Multiple hostnames can also be specified, separated
by spaces. The hostname can include an optional username in the form
`user@host`. When not specified options apply to all hosts, until the
first hostname specification is found. Note that matching of hostname is done
against the name you specify on the command line to connect to the remote host.
If you wish to include the same basic configuration for many different hosts,
you can do so with the [include](../../conf/#include) directive. In version 0.28.0
the behavior of this option was changed slightly, now, when a hostname is encountered
all its config values are set to defaults instead of being inherited from a previous
matching hostname block. In particular it means hostnames dont inherit configurations,
thereby avoiding hard to understand action-at-a-distance.

interpreter[¶](#opt-kitten-ssh.interpreter "Link to this definition")

```
interpreter sh
```

The interpreter to use on the remote host. Must be either a POSIX complaint
shell or a **python** executable. If the default **sh** is not
available or broken, using an alternate interpreter can be useful.

remote\_dir[¶](#opt-kitten-ssh.remote_dir "Link to this definition")

```
remote_dir .local/share/kitty-ssh-kitten
```

The location on the remote host where the files needed for this kitten are
installed. Relative paths are resolved with respect to `$HOME`. Absolute
paths have their leading / removed and so are also resolved with respect to $HOME.

copy[¶](#opt-kitten-ssh.copy "Link to this definition")

Copy files and directories from local to remote hosts. The specified files are
assumed to be relative to the HOME directory and copied to the HOME on the
remote. Directories are copied recursively. If absolute paths are used, they are
copied as is. For example:

```
copy .vimrc .zshrc .config/some-dir
```

Use `--dest` to copy a file to some other destination on the remote host:

```
copy --dest some-other-name some-file
```

Glob patterns can be specified to copy multiple files, with `--glob`:

```
copy --glob images/*.png
```

Files can be excluded when copying with `--exclude`:

```
copy --glob --exclude *.jpg --exclude *.bmp images/*
```

Files whose remote name matches the exclude pattern will not be copied.
For more details, see [The copy command](#ssh-copy-command).

## Login shell environment[¶](#login-shell-environment "Link to this heading")

shell\_integration[¶](#opt-kitten-ssh.shell_integration "Link to this definition")

```
shell_integration inherited
```

Control the shell integration on the remote host. See [Shell integration](../../shell-integration/#shell-integration)
for details on how this setting works. The special value `inherited` means
use the setting from `kitty.conf`. This setting is useful for overriding
integration on a per-host basis.

login\_shell[¶](#opt-kitten-ssh.login_shell "Link to this definition")

The login shell to execute on the remote host. By default, the remote user
account’s login shell is used.

env[¶](#opt-kitten-ssh.env "Link to this definition")

Specify the environment variables to be set on the remote host. Using the
name with an equal sign (e.g. `env VAR=`) will set it to the empty string.
Specifying only the name (e.g. `env VAR`) will remove the variable from
the remote shell environment. The special value `_kitty_copy_env_var_`
will cause the value of the variable to be copied from the local environment.
The definitions are processed alphabetically. Note that environment variables
are expanded recursively, for example:

```
env VAR1=a
env VAR2=${HOME}/${VAR1}/b
```

The value of `VAR2` will be `<path to home directory>/a/b`.

cwd[¶](#opt-kitten-ssh.cwd "Link to this definition")

The working directory on the remote host to change to. Environment variables in
this value are expanded. The default is empty so no changing is done, which
usually means the HOME directory is used.

color\_scheme[¶](#opt-kitten-ssh.color_scheme "Link to this definition")

Specify a color scheme to use when connecting to the remote host. If this option
ends with `.conf`, it is assumed to be the name of a config file to load
from the kitty config directory, otherwise it is assumed to be the name of a
color theme to load via the [themes kitten](../themes/). Note that
only colors applying to the text/background are changed, other config settings
in the .conf files/themes are ignored.

remote\_kitty[¶](#opt-kitten-ssh.remote_kitty "Link to this definition")

```
remote_kitty if-needed
```

Make **kitten** available on the remote host. Useful to run kittens such
as the [icat kitten](../icat/) to display images or the
[transfer file kitten](../transfer/) to transfer files. Only works if
the remote host has an architecture for which [pre-compiled kitten binaries](https://github.com/kovidgoyal/kitty/releases) are available. Note that kitten
is not actually copied to the remote host, instead a small bootstrap script is
copied which will download and run kitten when kitten is first executed on the
remote host. A value of `if-needed` means kitten is installed only if not
already present in the system-wide PATH. A value of `yes` means that kitten
is installed even if already present, and the installed kitten takes precedence.
Finally, `no` means no kitten is installed on the remote host. The
installed kitten can be updated by running: `kitten update-self` on the
remote host.

## SSH configuration[¶](#ssh-configuration "Link to this heading")

share\_connections[¶](#opt-kitten-ssh.share_connections "Link to this definition")

```
share_connections yes
```

Within a single kitty instance, all connections to a particular server can be
shared. This reduces startup latency for subsequent connections and means that
you have to enter the password only once. Under the hood, it uses SSH
ControlMasters and these are automatically cleaned up by kitty when it quits.
You can map a shortcut to [`close_shared_ssh_connections`](../../actions/#action-close_shared_ssh_connections) to disconnect all
active shared connections.

askpass[¶](#opt-kitten-ssh.askpass "Link to this definition")

```
askpass unless-set
```

Control the program SSH uses to ask for passwords or confirmation of host keys
etc. The default is to use kitty’s native **askpass**, unless the
[`SSH_ASKPASS`](../../glossary/#envvar-SSH_ASKPASS) environment variable is set. Set this option to
`ssh` to not interfere with the normal ssh askpass mechanism at all, which
typically means that ssh will prompt at the terminal. Set it to `native`
to always use kitty’s native, built-in askpass implementation. Note that not
using the kitty askpass implementation means that SSH might need to use the
terminal before the connection is established, so the kitten cannot use the
terminal to send data without an extra roundtrip, adding to initial connection
latency.

delegate[¶](#opt-kitten-ssh.delegate "Link to this definition")

Do not use the SSH kitten for this host. Instead run the command specified as the delegate.
For example using `delegate ssh` will run the ssh command with all arguments passed
to the kitten, except kitten specific ones. This is useful if some hosts are not capable
of supporting the ssh kitten.

forward\_remote\_control[¶](#opt-kitten-ssh.forward_remote_control "Link to this definition")

```
forward_remote_control no
```

Forward the kitty remote control socket to the remote host. This allows using the kitty
remote control facilities from the remote host. WARNING: This allows any software
on the remote host full access to the local computer, so only do it for trusted remote hosts.
Note that this does not work with abstract UNIX sockets such as `@mykitty` because of SSH limitations.
This option uses SSH socket forwarding to forward the socket pointed to by the [`KITTY_LISTEN_ON`](../../glossary/#envvar-KITTY_LISTEN_ON)
environment variable.

## Askpass automation[¶](#askpass-automation "Link to this heading")

password[¶](#opt-kitten-ssh.password "Link to this definition")

Specify a password to use when SSH prompts for a password. The value format is
“backend:secret”. Currently, only the “text” backend is supported, which stores
the secret in plain text in the config file. For example:

> password text:my\_password

If the backend prefix is omitted, it is treated as “text:” for backward
compatibility. Beware that storing passwords in plain text is insecure.

totp\_secret[¶](#opt-kitten-ssh.totp_secret "Link to this definition")

Specify a TOTP shared secret to auto-fill one-time codes when SSH asks for them.
The value format is “backend:secret”. Currently, only the “text” backend is
supported. For example:

> totp\_secret text:JBSWY3DPEHPK3PXP

If the backend prefix is omitted, it is treated as “text:” for backward
compatibility.

totp\_digits[¶](#opt-kitten-ssh.totp_digits "Link to this definition")

```
totp_digits 6
```

Number of digits for the generated TOTP codes. Default is 6.

totp\_period[¶](#opt-kitten-ssh.totp_period "Link to this definition")

```
totp_period 30
```

Time period in seconds for the TOTP code validity. Default is 30.

## The copy command[¶](#the-copy-command "Link to this heading")

```
copy [options] file-or-dir-to-copy ...
```

Copy files and directories from local to remote hosts. The specified files are
assumed to be relative to the HOME directory and copied to the HOME on the
remote. Directories are copied recursively. If absolute paths are used, they are
copied as is.

### Options[¶](#options "Link to this heading")

--glob [=no][¶](#cmdoption-glob "Link to this definition")
:   Interpret file arguments as glob patterns. Globbing is based on standard wildcards with the addition that `/**/` matches any number of directories. See the [detailed syntax](https://github.com/bmatcuk/doublestar#patterns).

--dest <DEST>[¶](#cmdoption-dest "Link to this definition")
:   The destination on the remote host to copy to. Relative paths are resolved relative to HOME on the remote host. When this option is not specified, the local file path is used as the remote destination (with the HOME directory getting automatically replaced by the remote HOME). Note that environment variables and ~ are not expanded.

--exclude <EXCLUDE>[¶](#cmdoption-exclude "Link to this definition")
:   A glob pattern. Files with names matching this pattern are excluded from being transferred. Only used when copying directories. Can be specified multiple times, if any of the patterns match the file will be excluded. If the pattern includes a `/` then it will match against the full path, not just the filename. In such patterns you can use `/**/` to match zero or more directories. For example, to exclude a directory and everything under it use `**/directory_name`. See the [detailed syntax](https://github.com/bmatcuk/doublestar#patterns) for how wildcards match.

--symlink-strategy <SYMLINK\_STRATEGY>[¶](#cmdoption-symlink-strategy "Link to this definition")
:   Control what happens if the specified path is a symlink. The default is to preserve the symlink, re-creating it on the remote machine. Setting this to `resolve` will cause the symlink to be followed and its target used as the file/directory to copy. The value of `keep-path` is the same as `resolve` except that the remote file path is derived from the symlink’s path instead of the path of the symlink’s target. Note that this option does not apply to symlinks encountered while recursively copying directories, those are always preserved.
    Default: `preserve`
    Choices: `keep-path`, `preserve`, `resolve`

## Copying terminfo files manually[¶](#copying-terminfo-files-manually "Link to this heading")

Sometimes, the ssh kitten can fail, or maybe you dont like to use it. In such
cases, the terminfo files can be copied over manually to a server with the
following one liner:

```
infocmp -a xterm-kitty | ssh myserver tic -x -o \~/.terminfo /dev/stdin
```

If you are behind a proxy (like Balabit) that prevents this, or you are SSHing
into macOS where the **tic** does not support reading from `STDIN`,
you must redirect the first command to a file, copy that to the server and run **tic**
manually. If you connect to a server, embedded, or Android system that doesn’t
have **tic**, copy over your local file terminfo to the other system as
`~/.terminfo/x/xterm-kitty`.

If the server is running a relatively modern Linux distribution and you have
root access to it, you could simply install the `kitty-terminfo` package on
the server to make the terminfo files available.

Really, the correct solution for this is to convince the OpenSSH maintainers to
have **ssh** do this automatically, if possible, when connecting to a
server, so that all terminals work transparently.

If the server is running FreeBSD, or another system that relies on termcap
rather than terminfo, you will need to convert the terminfo file on your local
machine by running (on local machine with *kitty*):

```
infocmp -CrT0 xterm-kitty
```

The output of this command is the termcap description, which should be appended
to `/usr/share/misc/termcap` on the remote server. Then run the following
command to apply your change (on the server):

```
cap_mkdb /usr/share/misc/termcap
```
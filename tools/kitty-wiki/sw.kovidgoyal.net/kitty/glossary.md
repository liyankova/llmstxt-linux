---
source_url: "https://sw.kovidgoyal.net/kitty/glossary/"
title: "Glossary - kitty"
crawl_date: "2025-11-16T14:51:00.313179Z"
selector: "article"
---

# Glossary - kitty

# Glossary[¶](#glossary "Link to this heading")

os\_window[¶](#term-os_window "Link to this term")
:   kitty has two kinds of windows. Operating System windows, referred to as [OS
    Window](#term-os_window), and *kitty windows*. An OS Window consists of one or more kitty
    [tabs](#term-tab). Each tab in turn consists of one or more *kitty
    windows* organized in a [layout](#term-layout).

tab[¶](#term-tab "Link to this term")
:   A *tab* refers to a group of [kitty windows](#term-window), organized in
    a [layout](#term-layout). Every [OS Window](#term-os_window) contains one or more tabs.

layout[¶](#term-layout "Link to this term")
:   A *layout* is a system of organizing [kitty windows](#term-window) in
    groups inside a tab. The layout automatically maintains the size and
    position of the windows, think of a layout as a tiling window manager for
    the terminal. See [Arrange windows](../layouts/) for details.

window[¶](#term-window "Link to this term")
:   kitty has two kinds of windows. Operating System windows, referred to as [OS
    Window](#term-os_window), and *kitty windows*. An OS Window consists of one or more kitty
    [tabs](#term-tab). Each tab in turn consists of one or more *kitty
    windows* organized in a [layout](#term-layout).

overlay[¶](#term-overlay "Link to this term")
:   An *overlay window* is a [kitty window](#term-window) that is placed on
    top of an existing kitty window, entirely covering it. Overlays are used
    throughout kitty, for example, to display the [the scrollback buffer](../overview/#scrollback),
    to display [hints](../kittens/hints/), for [unicode input](../kittens/unicode_input/) etc. Normal overlays are meant for short
    duration popups and so are not considered the active window
    when determining the current working directory or getting input text for
    kittens, launch commands, etc. To create an overlay considered as a
    main window use the `overlay-main` argument to
    [The launch command](../launch/).

hyperlinks[¶](#term-hyperlinks "Link to this term")
:   Terminals can have hyperlinks, just like the internet. In kitty you can
    [control exactly what happens](../open_actions/) when clicking on a
    hyperlink, based on the type of link and its URL. See also [Hyperlinks in terminal
    emulators](https://gist.github.com/egmontkob/eb114294efbcd5adb1944c9f3cb5feda).

kittens[¶](#term-kittens "Link to this term")
:   Small, independent statically compiled command line programs that are designed to run
    inside kitty windows and provide it with lots of powerful and flexible
    features such as viewing images, connecting conveniently to remote
    computers, transferring files, inputting unicode characters, etc.
    They can also be written by users in Python and used to customize and
    extend kitty functionality, see [Extend with kittens](../kittens_intro/) for details.

easing function[¶](#term-easing-function "Link to this term")
:   A function that controls how an animation progresses over time. kitty
    support the [CSS syntax for easing functions](https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function).
    Commonly used easing functions are `linear` for a constant rate
    animation and `ease-in-out` for an animation that starts slow,
    becomes fast in the middle and ends slowly. These are used to control
    various animations in kitty, such as [`cursor_blink_interval`](../conf/#opt-kitty.cursor_blink_interval) and
    [`visual_bell_duration`](../conf/#opt-kitty.visual_bell_duration).

## Environment variables[¶](#environment-variables "Link to this heading")

### Variables that influence kitty behavior[¶](#variables-that-influence-kitty-behavior "Link to this heading")

KITTY\_CONFIG\_DIRECTORY[¶](#envvar-KITTY_CONFIG_DIRECTORY "Link to this definition")
:   Controls where kitty looks for `kitty.conf` and other configuration
    files. Defaults to `~/.config/kitty`. For full details of the config
    directory lookup mechanism see, [`kitty --config`](../invocation/#cmdoption-kitty-config).

KITTY\_CACHE\_DIRECTORY[¶](#envvar-KITTY_CACHE_DIRECTORY "Link to this definition")
:   Controls where kitty stores cache files. Defaults to `~/.cache/kitty`
    or `~/Library/Caches/kitty` on macOS.

KITTY\_RUNTIME\_DIRECTORY[¶](#envvar-KITTY_RUNTIME_DIRECTORY "Link to this definition")
:   Controls where kitty stores runtime files like sockets. Defaults to
    the `XDG_RUNTIME_DIR` environment variable if that is defined
    otherwise the run directory inside the kitty cache directory is used.

VISUAL[¶](#envvar-VISUAL "Link to this definition")
:   The terminal based text editor (such as **vi** or **nano**)
    kitty uses, when, for instance, opening `kitty.conf` in response to
    [`ctrl+shift+f2`](../conf/#shortcut-kitty.Edit-config-file).

EDITOR[¶](#envvar-EDITOR "Link to this definition")
:   Same as [`VISUAL`](#envvar-VISUAL). Used if [`VISUAL`](#envvar-VISUAL) is not set.

SHELL[¶](#envvar-SHELL "Link to this definition")
:   Specifies the default shell kitty will run when [`shell`](../conf/#opt-kitty.shell) is set to
    `.`.

GLFW\_IM\_MODULE[¶](#envvar-GLFW_IM_MODULE "Link to this definition")
:   Set this to `ibus` to enable support for IME under X11.

KITTY\_WAYLAND\_DETECT\_MODIFIERS[¶](#envvar-KITTY_WAYLAND_DETECT_MODIFIERS "Link to this definition")
:   When set to a non-empty value, kitty attempts to autodiscover XKB modifiers
    under Wayland. This is useful if using non-standard modifiers like hyper. It
    is possible for the autodiscovery to fail; the default Wayland XKB mappings
    are used in this case. See [#3943](https://github.com/kovidgoyal/kitty/pull/3943) for details.

SSH\_ASKPASS[¶](#envvar-SSH_ASKPASS "Link to this definition")
:   Specify the program for SSH to ask for passwords. When this is set, [ssh
    kitten](../kittens/ssh/) will use this environment variable by default. See
    [`askpass`](../kittens/ssh/#opt-kitten-ssh.askpass) for details.

KITTY\_CLONE\_SOURCE\_CODE[¶](#envvar-KITTY_CLONE_SOURCE_CODE "Link to this definition")
:   Set this to some shell code that will be executed in the cloned window with
    `eval` when [clone-in-kitty](../shell-integration/#clone-shell) is used.

KITTY\_CLONE\_SOURCE\_PATH[¶](#envvar-KITTY_CLONE_SOURCE_PATH "Link to this definition")
:   Set this to the path of a file that will be sourced in the cloned window when
    [clone-in-kitty](../shell-integration/#clone-shell) is used.

KITTY\_DEVELOP\_FROM[¶](#envvar-KITTY_DEVELOP_FROM "Link to this definition")
:   Set this to the directory path of the kitty source code and its Python code
    will be loaded from there. Only works with official binary builds.

KITTY\_RC\_PASSWORD[¶](#envvar-KITTY_RC_PASSWORD "Link to this definition")
:   Set this to a pass phrase to use the `kitten @` remote control command with
    [`remote_control_password`](../conf/#opt-kitty.remote_control_password).

### Variables that kitty sets when running child programs[¶](#variables-that-kitty-sets-when-running-child-programs "Link to this heading")

LANG[¶](#envvar-LANG "Link to this definition")
:   This is only set on macOS. If the country and language from the macOS user
    settings form an invalid locale, it will be set to `en_US.UTF-8`.

PATH[¶](#envvar-PATH "Link to this definition")
:   kitty prepends itself to the PATH of its own environment to ensure the
    functions calling **kitty** will work properly.

KITTY\_WINDOW\_ID[¶](#envvar-KITTY_WINDOW_ID "Link to this definition")
:   An integer that is the id for the kitty [window](#term-window) the program is running in.
    Can be used with the [kitty remote control facility](../remote-control/).

KITTY\_PID[¶](#envvar-KITTY_PID "Link to this definition")
:   An integer that is the process id for the kitty process in which the program
    is running. Allows programs to tell kitty to reload its config by sending it
    the SIGUSR1 signal.

KITTY\_PUBLIC\_KEY[¶](#envvar-KITTY_PUBLIC_KEY "Link to this definition")
:   A public key that programs can use to communicate securely with kitty using
    the remote control protocol. The format is: `protocol:key data`.

WINDOWID[¶](#envvar-WINDOWID "Link to this definition")
:   The id for the [OS Window](#term-os_window) the program is running in. Only available
    on platforms that have ids for their windows, such as X11 and macOS.

TERM[¶](#envvar-TERM "Link to this definition")
:   The name of the terminal, defaults to `xterm-kitty`. See [`term`](../conf/#opt-kitty.term).

TERMINFO[¶](#envvar-TERMINFO "Link to this definition")
:   Path to a directory containing the kitty terminfo database. Or the terminfo
    database itself encoded in base64. See [`terminfo_type`](../conf/#opt-kitty.terminfo_type).

KITTY\_INSTALLATION\_DIR[¶](#envvar-KITTY_INSTALLATION_DIR "Link to this definition")
:   Path to the kitty installation directory.

COLORTERM[¶](#envvar-COLORTERM "Link to this definition")
:   Set to the value `truecolor` to indicate that kitty supports 16 million
    colors.

KITTY\_LISTEN\_ON[¶](#envvar-KITTY_LISTEN_ON "Link to this definition")
:   Set when the [remote control](../remote-control/) facility is enabled and
    the a socket is used for control via [`kitty --listen-on`](../invocation/#cmdoption-kitty-listen-on) or [`listen_on`](../conf/#opt-kitty.listen_on).
    Contains the path to the socket. Avoid the need to use [`kitten @ --to`](../remote-control/#cmdoption-kitten-to) when
    issuing remote control commands. Can also be a file descriptor of the form
    fd:num instead of a socket address, in which case, remote control
    communication should proceed over the specified file descriptor.

KITTY\_PIPE\_DATA[¶](#envvar-KITTY_PIPE_DATA "Link to this definition")
:   Set to data describing the layout of the screen when running child
    programs using [`launch --stdin-source`](../launch/#cmdoption-launch-stdin-source) with the contents of the
    screen/scrollback piped to them.

KITTY\_CHILD\_CMDLINE[¶](#envvar-KITTY_CHILD_CMDLINE "Link to this definition")
:   Set to the command line of the child process running in the kitty
    window when calling the notification callback program on terminal bell, see
    [`command_on_bell`](../conf/#opt-kitty.command_on_bell).

KITTY\_COMMON\_OPTS[¶](#envvar-KITTY_COMMON_OPTS "Link to this definition")
:   Set with the values of some common kitty options when running
    kittens, so kittens can use them without needing to load `kitty.conf`.

KITTY\_SHELL\_INTEGRATION[¶](#envvar-KITTY_SHELL_INTEGRATION "Link to this definition")
:   Set when enabling [Shell integration](../shell-integration/#shell-integration). It is automatically removed by
    the shell integration scripts.

KITTY\_SI\_RUN\_COMMAND\_AT\_STARTUP[¶](#envvar-KITTY_SI_RUN_COMMAND_AT_STARTUP "Link to this definition")
:   Set this to an expression that the kitty shell integration scripts will
    `eval` after the shell is started. Note that this environment variable
    is ignored when present in the environment in which kitty itself is launched
    in. It is most useful with the `--env` flag for the [launch](../launch/)
    action.

ZDOTDIR[¶](#envvar-ZDOTDIR "Link to this definition")
:   Set when enabling [Shell integration](../shell-integration/#shell-integration) with **zsh**, allowing
    **zsh** to automatically load the integration script.

XDG\_DATA\_DIRS[¶](#envvar-XDG_DATA_DIRS "Link to this definition")
:   Set when enabling [Shell integration](../shell-integration/#shell-integration) with **fish**, allowing
    **fish** to automatically load the integration script.

ENV[¶](#envvar-ENV "Link to this definition")
:   Set when enabling [Shell integration](../shell-integration/#shell-integration) with **bash**, allowing
    **bash** to automatically load the integration script.

KITTY\_OS[¶](#envvar-KITTY_OS "Link to this definition")
:   Set when using the include directive in kitty.conf. Can take values:
    `linux`, `macos`, `bsd`.

KITTY\_HOLD[¶](#envvar-KITTY_HOLD "Link to this definition")
:   Set to `1` when kitty is running a shell because of the `--hold` flag. Can
    be used to specialize shell behavior in the shell rc files as desired.

KITTY\_SIMD[¶](#envvar-KITTY_SIMD "Link to this definition")
:   Set it to `128` to use 128 bit vector registers, `256` to use 256 bit
    vector registers or any other value to prevent kitty from using SIMD CPU
    vector instructions. Warning, this overrides CPU capability detection so
    will cause kitty to crash with SIGILL if your CPU does not support the
    necessary SIMD extensions.
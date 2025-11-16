---
source_url: "https://sw.kovidgoyal.net/kitty/launch/"
title: "The launch command - kitty"
crawl_date: "2025-11-16T14:49:20.474225Z"
selector: "article"
---

# The launch command - kitty

# The **launch** command[¶](#the-launch-command "Link to this heading")

*kitty* has a `launch` action that can be used to run arbitrary programs
in new windows/tabs. It can be mapped to user defined shortcuts in
`kitty.conf`. It is very powerful and allows sending the contents of the
current window to the launched program, as well as many other options.

In the simplest form, you can use it to open a new kitty window running the
shell, as shown below:

```
map f1 launch
```

To run a different program simply pass the command line as arguments to launch:

```
map f1 launch vim path/to/some/file
```

To open a new window with the same working directory as the currently active
window:

```
map f1 launch --cwd=current
```

To open the new window in a new tab:

```
map f1 launch --type=tab
```

To run multiple commands in a shell, use:

```
map f1 launch sh -c "ls && exec zsh"
```

To pass the contents of the current screen and scrollback to the started
process:

```
map f1 launch --stdin-source=@screen_scrollback less
```

There are many more powerful options, refer to the complete list below.

Note

To avoid duplicating launch actions with frequently used parameters, you can
use [`action_alias`](../conf/#opt-kitty.action_alias) to define launch action aliases. For example:

```
action_alias launch_tab launch --cwd=current --type=tab
map f1 launch_tab vim
map f2 launch_tab emacs
```

The `F1` key will now open **vim** in a new tab with the current
windows working directory.

# The piping environment[¶](#the-piping-environment "Link to this heading")

When using [`launch --stdin-source`](#cmdoption-launch-stdin-source), the program to which the data is
piped has a special environment variable declared, [`KITTY_PIPE_DATA`](../glossary/#envvar-KITTY_PIPE_DATA)
whose contents are:

```
KITTY_PIPE_DATA={scrolled_by}:{cursor_x},{cursor_y}:{lines},{columns}
```

where `scrolled_by` is the number of lines kitty is currently scrolled by,
`cursor_(x|y)` is the position of the cursor on the screen with `(1,1)`
being the top left corner and `{lines},{columns}` being the number of rows
and columns of the screen.

# Special arguments[¶](#special-arguments "Link to this heading")

There are a few special placeholder arguments that can be specified as part of
the command line:

`@selection`
:   Replaced by the currently selected text.

`@active-kitty-window-id`
:   Replaced by the id of the currently active kitty window.

`@line-count`
:   Replaced by the number of lines in STDIN. Only present when passing some
    data to STDIN.

`@input-line-number`
:   Replaced by the number of lines a pager should scroll to match the current
    scroll position in kitty. See [`scrollback_pager`](../conf/#opt-kitty.scrollback_pager) for details.

`@scrolled-by`
:   Replaced by the number of lines kitty is currently scrolled by.

`@cursor-x`
:   Replaced by the current cursor x position with 1 being the leftmost cell.

`@cursor-y`
:   Replaced by the current cursor y position with 1 being the topmost cell.

`@first-line-on-screen`
:   Replaced by the first line on screen. Can be used for pager positioning.

`@last-line-on-screen`
:   Replaced by the last line on screen. Can be used for pager positioning.

For example:

```
map f1 launch my-program @active-kitty-window-id
```

# Watching launched windows[¶](#watching-launched-windows "Link to this heading")

The [`launch --watcher`](#cmdoption-launch-watcher) option allows you to specify Python functions
that will be called at specific events, such as when the window is resized or
closed. Note that you can also specify watchers that are loaded for all windows,
via [`watcher`](../conf/#opt-kitty.watcher). To create a watcher, specify the path to a Python module
that specifies callback functions for the events you are interested in, for
create `~/.config/kitty/mywatcher.py` and use [`launch --watcher`](#cmdoption-launch-watcher) = `mywatcher.py`:

```
# ~/.config/kitty/mywatcher.py
from typing import Any

from kitty.boss import Boss
from kitty.window import Window

def on_load(boss: Boss, data: dict[str, Any]) -> None:
    # This is a special function that is called just once when this watcher
    # module is first loaded, can be used to perform any initializztion/one
    # time setup. Any exceptions in this function are printed to kitty's
    # STDERR but otherwise ignored.
    ...

def on_resize(boss: Boss, window: Window, data: dict[str, Any]) -> None:
    # Here data will contain old_geometry and new_geometry
    # Note that resize is also called the first time a window is created
    # which can be detected as old_geometry will have all zero values, in
    # particular, old_geometry.xnum and old_geometry.ynum will be zero.
    ...

def on_focus_change(boss: Boss, window: Window, data: dict[str, Any])-> None:
    # Here data will contain focused
    ...

def on_close(boss: Boss, window: Window, data: dict[str, Any])-> None:
    # called when window is closed, typically when the program running in
    # it exits
    ...

def on_set_user_var(boss: Boss, window: Window, data: dict[str, Any]) -> None:
    # called when a "user variable" is set or deleted on a window. Here
    # data will contain key and value
    ...

def on_title_change(boss: Boss, window: Window, data: dict[str, Any]) -> None:
    # called when the window title is changed on a window. Here
    # data will contain title and from_child. from_child will be True
    # when a title change was requested via escape code from the program
    # running in the terminal
    ...

def on_cmd_startstop(boss: Boss, window: Window, data: dict[str, Any]) -> None:
    # called when the shell starts/stops executing a command. Here
    # data will contain is_start, cmdline and time.
    ...

def on_color_scheme_preference_change(boss: Boss, window: Window, data: dict[str, Any]) -> None:
    # called when the color scheme preference of this window changes from
    # light to dark or vice versa. data contains is_dark and via_escape_code
    # the latter will be true if the color scheme was changed via escape
    # code received from the program running in the window
    ...

def on_tab_bar_dirty(boss: Boss, window: Window, data: dict[str, Any]) -> None:
    # called when any changes happen to the tab bar, such a new tabs being
    # created, tab titles changing, tabs moving, etc. Useful to display the
    # tab bar externally to kitty. This is called even if the tab bar is
    # hidden. Note that this is called only in *global watchers*, that is
    # watchers defined in kitty.conf or using the --watcher command line
    # flag. data contains tab_manager which is the object responsible for
    # managing all tabs in a single OS Window.
    ...
```

Every callback is passed a reference to the global `Boss` object as well as
the `Window` object the action is occurring on. The `data` object is a dict
that contains event dependent data. You have full access to kitty internals in
the watcher scripts, however kitty internals are not documented/stable so for
most things you are better off using the kitty [Remote control API](../remote-control/).
Simply call `boss.call_remote_control()`, with the same arguments you
would pass to `kitten @`. For example:

```
def on_resize(boss: Boss, window: Window, data: dict[str, Any]) -> None:
    # send some text to the resized window
    boss.call_remote_control(window, ('send-text', f'--match=id:{window.id}', 'hello world'))
```

Run, `kitten @ --help` in a kitty terminal, to see all the remote control
commands available to you.

# Finding executables[¶](#finding-executables "Link to this heading")

When you specify a command to run as just a name rather than an absolute path,
it is searched for in the system-wide [`PATH`](../glossary/#envvar-PATH) environment variable. Note
that this **may not** be the value of [`PATH`](../glossary/#envvar-PATH) inside a shell, as shell
startup scripts often change the value of this variable. If it is not found
there, then a system specific list of default paths is searched. If it is still
not found, then your shell is run and the value of [`PATH`](../glossary/#envvar-PATH) inside the
shell is used.

See [`exe_search_path`](../conf/#opt-kitty.exe_search_path) for details and how to control this.

# Syntax reference[¶](#syntax-reference "Link to this heading")

```
launch [options] [program-to-run ...]
```

Launch an arbitrary program in a new kitty window/tab. Note that
if you specify a program-to-run you can use the special placeholder
`@selection` which will be replaced by the current selection.

## Options[¶](#options "Link to this heading")

--source-window <SOURCE\_WINDOW>[¶](#cmdoption-launch-source-window "Link to this definition")
:   A match expression to select the window from which data such as title, colors, env vars, screen contents, etc. are copied. When not specified the currently active window is used. See [Matching windows and tabs](../remote-control/#search-syntax) for the syntax used for specifying windows.

--title <WINDOW\_TITLE>, --window-title <WINDOW\_TITLE>[¶](#cmdoption-launch-title "Link to this definition")
:   The title to set for the new window. By default, title is controlled by the child process. The special value `current` will copy the title from the [`source window`](#cmdoption-launch-source-window).

--tab-title <TAB\_TITLE>[¶](#cmdoption-launch-tab-title "Link to this definition")
:   The title for the new tab if launching in a new tab. By default, the title of the active window in the tab is used as the tab title. The special value `current` will copy the title from the tab containing the [`source window`](#cmdoption-launch-source-window).

--type <TYPE>[¶](#cmdoption-launch-type "Link to this definition")
:   Where to launch the child process:

    `window`
    :   A new [kitty window](../glossary/#term-window) in the current tab

    `tab`
    :   A new [tab](../glossary/#term-tab) in the current OS window. Not available when the [launch](#) command is used in [startup sessions](../sessions/#sessions).

    `os-window`
    :   A new [operating system window](../glossary/#term-os_window). Not available when the [launch](#) command is used in [startup sessions](../sessions/#sessions).

    `overlay`
    :   An [overlay window](../glossary/#term-overlay) covering the current active kitty window

    `overlay-main`
    :   An [overlay window](../glossary/#term-overlay) covering the current active kitty window. Unlike a plain overlay window, this window is considered as a main window which means it is used as the active window for getting the current working directory, the input text for kittens, launch commands, etc. Useful if this overlay is intended to run for a long time as a primary window.

    `background`
    :   The process will be run in the background, without a kitty window. Note that if [`kitten @ launch --allow-remote-control`](../remote-control/#cmdoption-kitten-launch-allow-remote-control) is specified the [`KITTY_LISTEN_ON`](../glossary/#envvar-KITTY_LISTEN_ON) environment variable will be set to a dedicated socket pair file descriptor that the process can use for remote control.

    `clipboard`, `primary`
    :   These two are meant to work with [`--stdin-source`](#cmdoption-launch-stdin-source) to copy data to the system clipboard or primary selection.

    `os-panel`
    :   Similar to `os-window`, except that it creates the new OS Window as a desktop panel. Only works on platforms that support this, such as Wayand compositors that support the layer shell protocol. Use the [`kitten @ launch --os-panel`](../remote-control/#cmdoption-kitten-launch-os-panel) option to configure the panel.

    Default: `window`
    Choices: `background`, `clipboard`, `os-panel`, `os-window`, `overlay`, `overlay-main`, `primary`, `tab`, `window`

--dont-take-focus [=no], --keep-focus [=no][¶](#cmdoption-launch-dont-take-focus "Link to this definition")
:   Keep the focus on the currently active window instead of switching to the newly opened window.

--cwd <CWD>[¶](#cmdoption-launch-cwd "Link to this definition")
:   The working directory for the newly launched child. Use the special value `current` to use the working directory of the [`source window`](#cmdoption-launch-source-window) The special value `last_reported` uses the last working directory reported by the shell (needs [Shell integration](../shell-integration/#shell-integration) to work). The special value `oldest` works like `current` but uses the working directory of the oldest foreground process associated with the currently active window rather than the newest foreground process. Finally, the special value `root` refers to the process that was originally started when the window was created.

    When opening in the same working directory as the current window causes the new window to connect to a remote host, you can use the [`--hold-after-ssh`](#cmdoption-launch-hold-after-ssh) flag to prevent the new window from closing when the connection is terminated.

--add-to-session <ADD\_TO\_SESSION>[¶](#cmdoption-launch-add-to-session "Link to this definition")
:   Add the newly created window/tab to the specified session. Use `.` to add to the session of the [`source window`](#cmdoption-launch-source-window), if any. See [Sessions](../sessions/#sessions) for what a session is and how to use one. By default, the window is added to the session of the [`source window`](#cmdoption-launch-source-window) when [`launch --cwd`](#cmdoption-launch-cwd) is set to use the the working directory from that window, otherwise the newly created window does not belong to any session. To force adding to no session, use the value `!`. Adding a newly created window to a session is purely temporary, it does not change the actual session file, for that you have to resave the session. Note that using this flag in a launch command within a session file has no effect as the window is always added to the session belonging to that file.

--env <ENV>[¶](#cmdoption-launch-env "Link to this definition")
:   Environment variables to set in the child process. Can be specified multiple times to set different environment variables. Syntax: `name=value`. Using `name=` will set to empty string and just `name` will remove the environment variable.

--var <VAR>[¶](#cmdoption-launch-var "Link to this definition")
:   User variables to set in the created window. Can be specified multiple times to set different user variables. Syntax: `name=value`. Using `name=` will set to empty string.

--hold [=no][¶](#cmdoption-launch-hold "Link to this definition")
:   Keep the window open even after the command being executed exits, at a shell prompt. The shell will be run after the launched command exits.

--copy-colors [=no][¶](#cmdoption-launch-copy-colors "Link to this definition")
:   Set the colors of the newly created window to be the same as the colors in the [`source window`](#cmdoption-launch-source-window).

--copy-cmdline [=no][¶](#cmdoption-launch-copy-cmdline "Link to this definition")
:   Ignore any specified command line and instead use the command line from the [`source window`](#cmdoption-launch-source-window).

--copy-env [=no][¶](#cmdoption-launch-copy-env "Link to this definition")
:   Copy the environment variables from the [`source window`](#cmdoption-launch-source-window) into the newly launched child process. Note that this only copies the environment when the window was first created, as it is not possible to get updated environment variables from arbitrary processes. To copy that environment, use either the [clone-in-kitty](../shell-integration/#clone-shell) feature or the kitty remote control feature with [`kitten @ launch --copy-env`](../remote-control/#cmdoption-kitten-launch-copy-env).

--location <LOCATION>[¶](#cmdoption-launch-location "Link to this definition")
:   Where to place the newly created window when it is added to a tab which already has existing windows in it. `after` and `before` place the new window before or after the active window. `neighbor` is a synonym for `after`. Also applies to creating a new tab, where the value of `after` will cause the new tab to be placed next to the current tab instead of at the end. The values of `vsplit`, `hsplit` and `split` are only used by the `splits` layout and control if the new window is placed in a vertical, horizontal or automatic split with the currently active window. The default is to place the window in a layout dependent manner, typically, after the currently active window. See [`--next-to`](#cmdoption-launch-next-to) to use a window other than the currently active window.
    Default: `default`
    Choices: `after`, `before`, `default`, `first`, `hsplit`, `last`, `neighbor`, `split`, `vsplit`

--next-to <NEXT\_TO>[¶](#cmdoption-launch-next-to "Link to this definition")
:   A match expression to select the window next to which the new window is created. See [Matching windows and tabs](../remote-control/#search-syntax) for the syntax for specifying windows. If not specified defaults to the active window. When used via remote control and a target tab is specified this option is ignored unless the matched window is in the specified tab. When using [`--type`](#cmdoption-launch-type) of `tab`, the tab will be created in the OS Window containing the matched window.

--bias <BIAS>[¶](#cmdoption-launch-bias "Link to this definition")
:   The bias used to alter the size of the window. It controls what fraction of available space the window takes. The exact meaning of bias depends on the current layout.

    * Splits layout: The bias is interpreted as a percentage between 0 and 100. When splitting a window into two, the new window will take up the specified fraction of the space allotted to the original window and the original window will take up the remainder of the space.
    * Vertical/horizontal layout: The bias is interpreted as adding/subtracting from the normal size of the window. It should be a number between -90 and 90. This number is the percentage of the OS Window size that should be added to the window size. So for example, if a window would normally have been size 50 in the layout inside an OS Window that is size 80 high and --bias -10 is used it will become *approximately* size 42 high. Note that sizes are approximations, you cannot use this method to create windows of fixed sizes.
    * Tall layout: If the window being created is the *first* window in a column, then the bias is interpreted as a percentage, as for the splits layout, splitting the OS Window width between columns. If the window is a second or subsequent window in a column the bias is interpreted as adding/subtracting from the window size as for the vertical layout above.
    * Fat layout: Same as tall layout except it goes by rows instead of columns.
    * Grid layout: The bias is interpreted the same way as for the Vertical and Horizontal layouts, as something to be added/subtracted to the normal size. However, the since in a grid layout there are rows *and* columns, the bias on the first window in a column operates on the columns. Any later windows in that column operate on the row. So, for example, if you bias the first window in a grid layout it will change the width of the first column, the second window, the width of the second column, the third window, the height of the second row and so on.

    The bias option was introduced in kitty version 0.36.0.
    Default: `0`

--allow-remote-control [=no][¶](#cmdoption-launch-allow-remote-control "Link to this definition")
:   Programs running in this window can control kitty (even if remote control is not enabled in `kitty.conf`). Note that any program with the right level of permissions can still write to the pipes of any other program on the same computer and therefore can control kitty. It can, however, be useful to block programs running on other computers (for example, over SSH) or as other users. See [`--remote-control-password`](#cmdoption-launch-remote-control-password) for ways to restrict actions allowed by remote control.

--remote-control-password <REMOTE\_CONTROL\_PASSWORD>[¶](#cmdoption-launch-remote-control-password "Link to this definition")
:   Restrict the actions remote control is allowed to take. This works like [`remote_control_password`](../conf/#opt-kitty.remote_control_password). You can specify a password and list of actions just as for [`remote_control_password`](../conf/#opt-kitty.remote_control_password). For example:

    ```
    --remote-control-password '"my passphrase" get-* set-colors'
    ```

    This password will be in effect for this window only. Note that any passwords you have defined for [`remote_control_password`](../conf/#opt-kitty.remote_control_password) in `kitty.conf` are also in effect. You can override them by using the same password here. You can also disable all [`remote_control_password`](../conf/#opt-kitty.remote_control_password) global passwords for this window, by using:

    ```
    --remote-control-password '!'
    ```

    This option only takes effect if [`--allow-remote-control`](#cmdoption-launch-allow-remote-control) is also specified. Can be specified multiple times to create multiple passwords. This option was added to kitty in version 0.26.0

--stdin-source <STDIN\_SOURCE>[¶](#cmdoption-launch-stdin-source "Link to this definition")
:   Pass the screen contents as `STDIN` to the child process.

    `@selection`
    :   is the currently selected text in the [`source window`](#cmdoption-launch-source-window).

    `@screen`
    :   is the contents of the [`source window`](#cmdoption-launch-source-window).

    `@screen_scrollback`
    :   is the same as `@screen`, but includes the scrollback buffer as well.

    `@alternate`
    :   is the secondary screen of the [`source window`](#cmdoption-launch-source-window). For example if you run a full screen terminal application, the secondary screen will be the screen you return to when quitting the application.

    `@first_cmd_output_on_screen`
    :   is the output from the first command run in the shell on screen.

    `@last_cmd_output`
    :   is the output from the last command run in the shell.

    `@last_visited_cmd_output`
    :   is the first output below the last scrolled position via [`scroll_to_prompt`](../actions/#action-scroll_to_prompt), this needs [shell integration](../shell-integration/#shell-integration) to work.

    Default: `none`
    Choices: `@alternate`, `@alternate_scrollback`, `@first_cmd_output_on_screen`, `@last_cmd_output`, `@last_visited_cmd_output`, `@screen`, `@screen_scrollback`, `@selection`, `none`

--stdin-add-formatting [=no][¶](#cmdoption-launch-stdin-add-formatting "Link to this definition")
:   When using [`--stdin-source`](#cmdoption-launch-stdin-source) add formatting escape codes, without this only plain text will be sent.

--stdin-add-line-wrap-markers [=no][¶](#cmdoption-launch-stdin-add-line-wrap-markers "Link to this definition")
:   When using [`--stdin-source`](#cmdoption-launch-stdin-source) add a carriage return at every line wrap location (where long lines are wrapped at screen edges). This is useful if you want to pipe to program that wants to duplicate the screen layout of the screen.

--marker <MARKER>[¶](#cmdoption-launch-marker "Link to this definition")
:   Create a marker that highlights text in the newly created window. The syntax is the same as for the [`toggle_marker`](../actions/#action-toggle_marker) action (see [Mark text on screen](../marks/)).

--os-window-class <OS\_WINDOW\_CLASS>[¶](#cmdoption-launch-os-window-class "Link to this definition")
:   Set the WM\_CLASS property on X11 and the application id property on Wayland for the newly created OS window when using [`--type=os-window`](#cmdoption-launch-type). Defaults to whatever is used by the parent kitty process, which in turn defaults to `kitty`.

--os-window-name <OS\_WINDOW\_NAME>[¶](#cmdoption-launch-os-window-name "Link to this definition")
:   Set the WM\_NAME property on X11 for the newly created OS Window when using [`--type=os-window`](#cmdoption-launch-type). Defaults to [`--os-window-class`](#cmdoption-launch-os-window-class).

--os-window-title <OS\_WINDOW\_TITLE>[¶](#cmdoption-launch-os-window-title "Link to this definition")
:   Set the title for the newly created OS window. This title will override any titles set by programs running in kitty. The special value `current` will copy the title from the OS Window containing the [`source window`](#cmdoption-launch-source-window).

--os-window-state <OS\_WINDOW\_STATE>[¶](#cmdoption-launch-os-window-state "Link to this definition")
:   The initial state for the newly created OS Window.
    Default: `normal`
    Choices: `fullscreen`, `maximized`, `minimized`, `normal`

--logo <LOGO>[¶](#cmdoption-launch-logo "Link to this definition")
:   Path to a PNG image to use as the logo for the newly created window. See [`window_logo_path`](../conf/#opt-kitty.window_logo_path). Relative paths are resolved from the kitty configuration directory.

--logo-position <LOGO\_POSITION>[¶](#cmdoption-launch-logo-position "Link to this definition")
:   The position for the window logo. Only takes effect if [`--logo`](#cmdoption-launch-logo) is specified. See [`window_logo_position`](../conf/#opt-kitty.window_logo_position).

--logo-alpha <LOGO\_ALPHA>[¶](#cmdoption-launch-logo-alpha "Link to this definition")
:   The amount the window logo should be faded into the background. Only takes effect if [`--logo`](#cmdoption-launch-logo) is specified. See [`window_logo_alpha`](../conf/#opt-kitty.window_logo_alpha).
    Default: `-1`

--color <COLOR>[¶](#cmdoption-launch-color "Link to this definition")
:   Change colors in the newly launched window. You can either specify a path to a `.conf` file with the same syntax as `kitty.conf` to read the colors from, or specify them individually, for example:

    ```
    --color background=white --color foreground=red
    ```

--spacing <SPACING>[¶](#cmdoption-launch-spacing "Link to this definition")
:   Set the margin and padding for the newly created window. For example: `margin=20` or `padding-left=10` or `margin-h=30`. The shorthand form sets all values, the `*-h` and `*-v` variants set horizontal and vertical values. Can be specified multiple times. Note that this is ignored for overlay windows as these use the settings from the base window.

--watcher <WATCHER>, -w <WATCHER>[¶](#cmdoption-launch-watcher "Link to this definition")
:   Path to a Python file. Appropriately named functions in this file will be called for various events, such as when the window is resized, focused or closed. See the section on watchers in the launch command documentation: [Watching launched windows](#watchers). Relative paths are resolved relative to the [kitty config directory](../conf/#confloc). Global watchers for all windows can be specified with [`watcher`](../conf/#opt-kitty.watcher) in `kitty.conf`.

--os-panel <OS\_PANEL>[¶](#cmdoption-launch-os-panel "Link to this definition")
:   Options to control the creation of desktop panels. Takes the same settings as the [panel kitten](../kittens/panel/), except for [`--override`](../kittens/panel/#cmdoption-kitty-kitten-panel-override) and [`--config`](../kittens/panel/#cmdoption-kitty-kitten-panel-config). Can be specified multiple times. For example, to create a desktop panel at the bottom of the screen two lines high:

    ```
    launch --type os-panel --os-panel lines=2 --os-panel edge=bottom sh -c "echo; echo; echo hello; sleep 5s"
    ```

--hold-after-ssh [=no][¶](#cmdoption-launch-hold-after-ssh "Link to this definition")
:   When using [`--cwd`](#cmdoption-launch-cwd)`=current` or similar from a window that is running the ssh kitten, the new window will run a local shell after disconnecting from the remote host, when this option is specified.
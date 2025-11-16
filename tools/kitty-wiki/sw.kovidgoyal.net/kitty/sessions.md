---
source_url: "https://sw.kovidgoyal.net/kitty/sessions/"
title: "Sessions - kitty"
crawl_date: "2025-11-16T14:49:43.942919Z"
selector: "article"
---

# Sessions - kitty

# Sessions[¶](#sessions "Link to this heading")

kitty has robust support for sessions. A session is basically a simple text
file where you can define kitty windows, tabs and what programs to run in them
as well as how to layout the windows. kitty also supports actions to easily
[`create and switch between existing sessions`](../actions/#action-goto_session), so that you
can move seamlessly from working on one project to another with a couple of keystrokes.

Let’s see a quick example to get a feel of how easy it is to create sessions. First,
a session file to develop a project:

```
# Set the layout for the current tab
layout tall
# Set the working directory for windows in the current tab
cd ~/path/to/myproject
# Create the "main" window and run an editor in it to edit the project files
launch --title "Edit My Project" /usr/bin/nvim
# Create a side window to run a shell to build or test project
launch --title "Build My Project"
# Create another side window to keep an eye on some useful log file
launch --title "Log for my project" /usr/bin/tail -f /path/to/project/log/file
```

Save this file as `~/path/to/myproject/launch.kitty-session`. Now when
you want to work on the project, simply run:

```
kitty --session ~/path/to/myproject/launch.kitty-session
```

You can also set the session in `kitty.conf` via [`startup_session`](../conf/#opt-kitty.startup_session).

Thus, it is very easy to create sessions and work on projects. To learn how to
create more complex sessions, see [More complex sessions](#complex-sessions).

## Creating/Switching to sessions with a keypress[¶](#creating-switching-to-sessions-with-a-keypress "Link to this heading")

If you like to manage multiple sessions within a single terminal and
easily swap between them, kitty has you covered. You can use the
[`goto_session`](../actions/#action-goto_session) action in kitty.conf, like this:

```
# Press F7 and then c to jump to the "cool" project
map f7>c goto_session ~/path/to/cool/cool.kitty-session
# Press F7 and then h to jump to the "hot" project
map f7>h goto_session ~/path/to/hot/hot.kitty-session
# Browse and select from the list of known projects defined via goto_session commands
map f7>/ goto_session
# Same as above, but the sessions are listed alphabetically instead of by most recent
map f7>/ goto_session --sort-by=alphabetical
# Go to the previously active session (larger negative numbers jump further back in history)
map f7>- goto_session -1
```

In this manner you can define as many projects/sessions as you like and easily
switch between them with a keypress.

You can also close sessions using the [`close_session`](../actions/#action-close_session) action, which closes
all windows in the session with a single keypress.

## Displaying the currently active session name[¶](#displaying-the-currently-active-session-name "Link to this heading")

You can display the name of the currently active session file in the kitty tab
bar using [`tab_title_template`](../conf/#opt-kitty.tab_title_template). For example, using the value:

```
{session_name} {title}
```

will show you the name of the session file the current tab was loaded from, as
well as the normal tab title. Or alternatively, you can set the tab title
directly to a project name in the session file itself when creating the tab,
like this:

```
new_tab My Project Name
```

## More complex sessions[¶](#more-complex-sessions "Link to this heading")

If you want to create more complex sessions, with sophisticated layouts, such
as [The Splits Layout](../layouts/#splits-layout), the easiest way is to set up the state you want to
save manually by first starting kitty like this:

```
kitty -o 'map f1 save_as_session --use-foreground-process --relocatable'
```

Now create whatever splits and tabs you need and start whatever programs such
as editors, REPLs, debuggers, etc. you want to start in each of them. Once
kitty is the way you want it, press the `F1` key, and you will be prompted
for a path at which to save the session file. Specify the path and the session
will be saved there with the exact setup you created. The saved file will even
be opened in your editor for you to review, automatically.

Tip

If you want session files to be saved to a specific directory regardless of
your current working directory, use the `--base-dir` option. For example:

```
map f7>s save_as_session --use-foreground-process --base-dir ~/.local/share/kitty/sessions
```

This is particularly useful when kitty is launched from system-wide shortcuts
where the working directory might not be your home directory. Note that
`--relocatable` is typically not used with `--base-dir`, since relocatable
is meant for session files that are co-located with their project directories.

If instead, you want to create these by hand, see the example below which shows
all the major keywords you can use in kitty session files:

```
# Set the layout for the current tab
layout tall
# Set the working directory for windows in the current tab. Relative paths
# are resolved with respect to the location of this session file.
cd ~
# Create a window and run the specified command in it
launch zsh
# Create a window with some environment variables set and run vim in it
launch --env FOO=BAR vim
# Set the title for the next window
launch --title "Chat with x" irssi --profile x
# Run a short lived command and see its output
launch --hold message-of-the-day

# Create a new tab
# The part after new_tab is the optional tab title which will be displayed in
# the tab bar, if omitted, the title of the active window will be used instead.
new_tab my tab
cd somewhere
# Set the layouts allowed in this tab
enabled_layouts tall,stack
# Set the current layout
layout stack
launch zsh

# Create a new OS window
# Any definitions specified before the first new_os_window will apply to first OS window.
new_os_window
# Set new window size to 80x24 cells
os_window_size 80c 24c
# Set the --title for the new OS window
os_window_title my fancy os window
# Set the --class for the new OS window
os_window_class mywindow
# Set the --name for the new OS window
os_window_name myname
# Change the OS window state to normal, fullscreen, maximized or minimized
os_window_state normal
launch sh
# Resize the current window (see the resize_window action for details)
resize_window wider 2
# Make the current window the active (focused) window in its tab
focus
# Make the current OS Window the globally active window
focus_os_window
launch emacs

# Create another tab
new_tab logs
launch tail -f /var/log/syslog

# Focus the first tab (index 0) when the session loads
# You can also use a match expression like: focus_tab title:logs
focus_tab 0

# Create a complex layout using multiple splits. Creates two columns of
# windows with two windows in each column. The windows in the first column are
# split 50:50. In the second column the windows are not evenly split.
new_tab complex tab
layout splits
# First window, set a user variable on it so we can focus it later
launch --var window=first
# Create the second column by splitting the first window vertically
launch --location=vsplit
# Create the third window in the second column by splitting the second window horizontally
# Make it take 40% of the height instead of 50%
launch --location=hsplit --bias=40
# Go back to focusing the first window, so that we can split it
focus_matching_window var:window=first
# Create the final window in the first column
launch --location=hsplit
```

Note

The [launch](../launch/) command when used in a session file cannot create
new OS windows, or tabs.

Note

Environment variables of the form `${NAME}` or `$NAME` are
expanded in the session file, except in the *arguments* (not options) to the
launch command. For example:

```
launch --cwd=$THIS_IS_EXPANDED some-program $THIS_IS_NOT_EXPANDED
```

## Making newly created windows join an existing session[¶](#making-newly-created-windows-join-an-existing-session "Link to this heading")

Normally, after activating a session, if you create new windows/tabs
they don’t belong to the session. If you would prefer to have them belong
to the currently active session, you can use the [`new_window_with_cwd`](../actions/#action-new_window_with_cwd)
and [`new_tab_with_cwd`](../actions/#action-new_tab_with_cwd) actions instead, like this:

```
map kitty_mod+enter new_window_with_cwd
map kitty_mod+t new_tab_with_cwd
map kitty_mod+n new_os_window_with_cwd
```

This will cause newly created windows and tabs to belong to the currently active
session, if any. Note that adding a window to a session in this way is
temporary, it does not edit the session file. If you wish to update the
session file of the currently active session, you can use the following
mapping for it:

```
map f5 save_as_session --relocatable --use-foreground-process --match=session:. .
```

The two can be combined, using the [`combine`](../actions/#action-combine) action.
For even more control of what session a window is added to use
the [launch](../launch/) command with the [`launch --add-to-session`](../launch/#cmdoption-launch-add-to-session)
flag.

## Sessions with remote connections[¶](#sessions-with-remote-connections "Link to this heading")

If you use the [ssh kitten](../kittens/ssh/) to connect to remote computers,
[`save_as_session`](../actions/#action-save_as_session) is smart enough to save the ssh kitten invocation to your
session file, preserving the remote working directory and even the currently
running program on the remote host! Try it, run kitty with:

```
kitty -o 'map f1 save_as_session --use-foreground-process --relocatable' --session <(echo "layout vertical\nlaunch\nlaunch")
```

Now in both windows, run:

```
kitten ssh localhost
```

To connect them both to a remote computer (replace `localhost` with another
computer if you like). In one window change the directory to /tmp and in the
other start some program. Then press `F1` to save the session file.
When you run the session file in another kitty instance you will see both
windows re-created, as expected with the correct working directories and
running programs.

## Managing multi tab sessions in a single OS Window[¶](#managing-multi-tab-sessions-in-a-single-os-window "Link to this heading")

The natural way to organise sessions in kitty is one per [os\_window](../glossary/#term-os_window).
However, if you prefer to manage multiple sessions in a single OS Window, you
can configure the kitty tab bar to only show tabs that belong to the currently
active session. To do so, use [`tab_bar_filter`](../conf/#opt-kitty.tab_bar_filter) in `kitty.conf` set:

```
tab_bar_filter session:~ or session:^$
```

This will restrict the tab bar to only showing tabs from the currently active
session as well tabs that do not belong to any session. Furthermore, when you
are in a window or tab that does not belong to any session, the tab bar will
show the tabs from the most recent active session, to maintain context.

## Keyword reference[¶](#keyword-reference "Link to this heading")

Below is the list of all supported keywords in session files along with
documentation for them.

`cd [path]`
:   Change the working directory for all windows in the current tab to
    `path`. Relative paths are resolved with respect to the directory
    containing the session file.

`focus`
:   Give keyboard focus to the window created by the previous launch command

`focus_matching_window`
:   Give keyboard focus to window that matches the specified expression. See
    [Matching windows and tabs](../remote-control/#search-syntax) for the syntax for matching expressions.

`focus_os_window`
:   Give keyboard focus to the current OS Window. This is guaranteed to work
    only is some other OS Window in the current kitty process has focus,
    otherwise the window manager might block changing focus to prevent *focus
    stealing*.

`focus_tab [tab specifier]`
:   Set which tab should be active (focused) in the current OS Window. The tab
    specifier can be either a plain number (treated as a 0-based index) or a
    match expression. For example, `focus_tab 0` will focus the first tab,
    `focus_tab 1` the second tab, and `focus_tab title:logs` will focus the
    tab whose title matches “logs”. See [Matching windows and tabs](../remote-control/#search-syntax) for the full syntax
    of match expressions. This is useful for session files that create multiple
    tabs and want to ensure a specific tab is active when the session is loaded.

`enabled_layouts comma separated list of layout names`
:   Set the layouts allowed in the current tab. Same syntax as
    [`enabled_layouts`](../conf/#opt-kitty.enabled_layouts).

`launch`
:   Create a new window running the specified command or the default shell if
    no command is specified. See [The launch command](../launch/) for details. Note that creating
    tabs and OS Windows using launch is not supported in session files, use the
    dedicated keywords for these.

`layout name`
:   Set the layout for the current tab to the specified layout, including any
    specified options, see [Arrange windows](../layouts/) for the available alyouts and
    options.

`new_os_window`
:   Create a new OS Window. Any OS window related keywords specified before the
    first `new_os_window` will apply to the first OS Window.

`new_tab [tab title]`
:   Create a new tab with the specified title. If no title is specified, the
    title behaves just as for a regular tab in kitty.

`os_window_title`
:   Set the title for the current OS Window. The OS Window will then always
    have this title, it will not change based on the title of the currently active
    window inside the OS Window.

`os_window_class`
:   Set the class part of WM\_CLASS or Wayland Application Id for the current OS Window

`os_window_name`
:   Set the name part of WM\_CLASS or Wayland Window tag for the current OS Window

`os_window_size`
:   Set the size of the current OS Window, can be specified in pixels or cells.
    For example: 80c 24c is a window of width 80 cells by 24 cells.

`os_window_state`
:   Set the state of the current OS Window, can be: `normal`, `fullscreen`, `maximized` or `minimized`

`resize_window`
:   Resize the current window. See the [`resize_window`](../actions/#action-resize_window) action for details.
    For example: resize\_window wider 2

`set_layout_state`
:   This keyword is only used in session files generated by the
    [`save_as_session`](../actions/#action-save_as_session) action, it’s syntax is undocumented and for internal
    use only.

`title`
:   Set the title for the next window. Deprecated, use `launch --title`
    instead.

## The save\_as\_session action[¶](#the-save-as-session-action "Link to this heading")

This action can be mapped to a key press in `kitty.conf`. It will save
the currently open OS Windows, tabs, windows, running programs, working
directories, etc. into a session file. It is a convenient way to
[More complex sessions](#complex-sessions). The options this action takes are documented below.

```
save_as_session [options] [path-to-save-session-file-at]
```

Save the current state of kitty as a session file for easy re-use. If the path at which to save the session
file is not specified, kitty will prompt you for one. If the path is `.` it will save the session
to the path of the currently active session, if there is one, otherwise prompt you for a path.

### Options[¶](#options "Link to this heading")

--save-only [=no][¶](#cmdoption-save-only "Link to this definition")
:   Only save the specified session file, dont open it in an editor to review after saving.

--use-foreground-process [=no][¶](#cmdoption-use-foreground-process "Link to this definition")
:   When saving windows that were started with the default shell but are currently running some other process inside that shell, save that process so that when the session is used both the shell **and** the process running inside it are re-started. This is most useful when you have opened programs like editors or similar inside windows that started out running the shell and you want to preserve that. WARNING: Be careful when using this option, if you are running some dangerous command like `rm` or `mv` or similar in a shell, it will be re-run when the session is executed if you use this option. Note that this option requires [Shell integration](../shell-integration/#shell-integration) to work.

--relocatable [=no][¶](#cmdoption-relocatable "Link to this definition")
:   When saving the working directory for windows, do so as paths relative to the directory in which the session file will be saved. This allows the session file to work even when its containing directory is moved elsewhere.

--match <MATCH>[¶](#cmdoption-match "Link to this definition")
:   If specified, only save all windows (and their parent tabs/OS Windows) that match the specified search expression. See [Matching windows and tabs](../remote-control/#search-syntax) for details on the search language. In particular if you want to only save windows that are present in the currently active session, use `--match=session:.`.

--base-dir <BASE\_DIR>[¶](#cmdoption-base-dir "Link to this definition")
:   When specified, relative session filenames will be saved to this directory instead of the current working directory. This is useful when kitty is launched from locations where the working directory is not your home directory, such as from system-wide shortcuts. Note that `--relocatable` is typically not used with `--base-dir`, since relocatable is meant for session files that are co-located with their project directories.
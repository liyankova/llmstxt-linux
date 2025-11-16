---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/broadcast/"
title: "broadcast - kitty"
crawl_date: "2025-11-16T14:48:44.285086Z"
selector: "article"
---

# broadcast - kitty

# broadcast[¶](#broadcast "Link to this heading")

*Type text in all kitty windows simultaneously*

The `broadcast` kitten can be used to type text simultaneously in all
[kitty windows](../../glossary/#term-window) (or a subset as desired).

To use it, simply create a mapping in `kitty.conf` such as:

```
map f1 launch --allow-remote-control kitty +kitten broadcast
```

Then press the `F1` key and whatever you type in the newly created window
will be sent to all kitty windows.

You can use the options described below to control which windows are selected.

For example, only broadcast to other windows in the current tab:

```
map f1 launch --allow-remote-control kitty +kitten broadcast --match-tab state:focused
```

## Source code for broadcast[¶](#source-code-for-broadcast "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/broadcast).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitty +kitten broadcast [options] [initial text to send ...]
```

Broadcast typed text to kitty windows. By default text is sent to all windows, unless one of the matching options is specified

### Options[¶](#options "Link to this heading")

--hide-input-toggle <HIDE\_INPUT\_TOGGLE>[¶](#cmdoption-kitty-kitten-broadcast-hide-input-toggle "Link to this definition")
:   Key to press that will toggle hiding of the input in the broadcast window itself. Useful while typing a password, prevents the password from being visible on the screen.
    Default: `Ctrl+Alt+Esc`

--end-session <END\_SESSION>[¶](#cmdoption-kitty-kitten-broadcast-end-session "Link to this definition")
:   Key to press to end the broadcast session.
    Default: `Ctrl+Esc`

--match <MATCH>, -m <MATCH>[¶](#cmdoption-kitty-kitten-broadcast-match "Link to this definition")
:   The window to match. Match specifications are of the form: field:query. Where field can be one of: `id`, `title`, `pid`, `cwd`, `cmdline`, `num`, `env`, `var`, `state`, `neighbor`, `session` and `recent`. query is the expression to match. Expressions can be either a number or a regular expression, and can be [combined using Boolean operators](../../remote-control/#search-syntax).

    The special value `all` matches all windows.

    For numeric fields: `id`, `pid`, `num` and `recent`, the expression is interpreted as a number, not a regular expression. Negative values for `id` match from the highest id number down, in particular, -1 is the most recently created window.

    The field `num` refers to the window position in the current tab, starting from zero and counting clockwise (this is the same as the order in which the windows are reported by the [kitten @ ls](../../remote-control/#at-ls) command).

    The window id of the current window is available as the [`KITTY_WINDOW_ID`](../../glossary/#envvar-KITTY_WINDOW_ID) environment variable.

    The field `recent` refers to recently active windows in the currently active tab, with zero being the currently active window, one being the previously active window and so on.

    The field `neighbor` refers to a neighbor of the active window in the specified direction, which can be: `left`, `right`, `top` or `bottom`.

    The field `session` matches windows that were created in the specified session. Use the expression `^$` to match windows that were not created in a session and `.` to match the currently active session and `~` to match either the currently active sesison or the last active session when no session is active.

    When using the `env` field to match on environment variables, you can specify only the environment variable name or a name and value, for example, `env:MY_ENV_VAR=2`.

    Similarly, the `var` field matches on user variables set on the window. You can specify name or name and value as with the `env` field.

    The field `state` matches on the state of the window. Supported states are: `active`, `focused`, `needs_attention`, `parent_active`, `parent_focused`, `focused_os_window`, `self`, `overlay_parent`. Active windows are the windows that are active in their parent tab. There is only one focused window and it is the window to which keyboard events are delivered. If no window is focused, the last focused window is matched. The value `focused_os_window` matches all windows in the currently focused OS window. The value `self` matches the window in which the remote control command is run. The value `overlay_parent` matches the window that is under the `self` window, when the self window is an overlay.

    Note that you can use the [kitten @ ls](../../remote-control/#at-ls) command to get a list of windows.

--match-tab <MATCH\_TAB>, -t <MATCH\_TAB>[¶](#cmdoption-kitty-kitten-broadcast-match-tab "Link to this definition")
:   The tab to match. Match specifications are of the form: field:query. Where field can be one of: `id`, `index`, `title`, `window_id`, `window_title`, `pid`, `cwd`, `cmdline` `env`, `var`, `state`, `session` and `recent`. query is the expression to match. Expressions can be either a number or a regular expression, and can be [combined using Boolean operators](../../remote-control/#search-syntax).

    The special value `all` matches all tabs.

    For numeric fields: `id`, `index`, `window_id`, `pid` and `recent`, the expression is interpreted as a number, not a regular expression. Negative values for `id`/`window_id` match from the highest id number down, in particular, -1 is the most recently created tab/window.

    When using `title` or `id`, first a matching tab is looked for, and if not found a matching window is looked for, and the tab for that window is used.

    You can also use `window_id` and `window_title` to match the tab that contains the window with the specified id or title.

    The `index` number is used to match the nth tab in the currently active OS window. The `recent` number matches recently active tabs in the currently active OS window, with zero being the currently active tab, one the previously active tab and so on.

    The field `session` matches tabs that were created in the specified session. Use the expression `^$` to match windows that were not created in a session and `.` to match the currently active session and `~` to match either the currently active sesison or the last active session when no session is active.

    When using the `env` field to match on environment variables, you can specify only the environment variable name or a name and value, for example, `env:MY_ENV_VAR=2`. Tabs containing any window with the specified environment variables are matched. Similarly, `var` matches tabs containing any window with the specified user variable.

    The field `state` matches on the state of the tab. Supported states are: `active`, `focused`, `needs_attention`, `parent_active`, `parent_focused` and `focused_os_window`. Active tabs are the tabs that are active in their parent OS window. There is only one focused tab and it is the tab to which keyboard events are delivered. If no tab is focused, the last focused tab is matched. The value `focused_os_window` matches all tabs in the currently focused OS window.

    Note that you can use the [kitten @ ls](../../remote-control/#at-ls) command to get a list of tabs.
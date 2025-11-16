---
source_url: "https://sw.kovidgoyal.net/kitty/rc_protocol/"
title: "The kitty remote control protocol - kitty"
crawl_date: "2025-11-16T14:49:16.692832Z"
selector: "article"
---

# The kitty remote control protocol - kitty

# The kitty remote control protocol[¶](#the-kitty-remote-control-protocol "Link to this heading")

The kitty remote control protocol is a simple protocol that involves sending
data to kitty in the form of JSON. Any individual command of kitty has the
form:

```
<ESC>P@kitty-cmd<JSON object><ESC>\
```

Where `<ESC>` is the byte `0x1b`. The JSON object has the form:

```
{
    "cmd": "command name",
    "version": "<kitty version>",
    "no_response": "<Optional Boolean>",
    "kitty_window_id": "<Optional value of the KITTY_WINDOW_ID env var>",
    "payload": "<Optional JSON object>"
}
```

The `version` above is an array of the form `[0, 14, 2]`. If you are
developing a standalone client, use the kitty version that you are developing
against. Using a version greater than the version of the kitty instance you are
talking to, will cause a failure.

Set `no_response` to `true` if you don’t want a response from kitty.

The optional payload is a JSON object that is specific to the actual command
being sent. The fields in the object for every command are documented below.

As a quick example showing how easy to use this protocol is, we will implement
the `@ ls` command from the shell using only shell tools.

First, run kitty as:

```
kitty -o allow_remote_control=socket-only --listen-on unix:/tmp/test
```

Now, in a different terminal, you can get the pretty printed `@ ls` output
with the following command line:

```
echo -en '\eP@kitty-cmd{"cmd":"ls","version":[0,14,2]}\e\\' | socat - unix:/tmp/test | awk '{ print substr($0, 13, length($0) - 14) }' | jq -c '.data | fromjson' | jq .
```

There is also the statically compiled stand-alone executable `kitten`
that can be used for this, available from the [kitty releases](https://github.com/kovidgoyal/kitty/releases) page:

```
kitten @ --help
```

## Encrypted communication[¶](#encrypted-communication "Link to this heading")

Added in version 0.26.0.

When using the [`remote_control_password`](../conf/#opt-kitty.remote_control_password) option communication to the
terminal is encrypted to keep the password secure. A public key is used from
the [`KITTY_PUBLIC_KEY`](../glossary/#envvar-KITTY_PUBLIC_KEY) environment variable. Currently, only one
encryption protocol is supported. The protocol number is present in
[`KITTY_PUBLIC_KEY`](../glossary/#envvar-KITTY_PUBLIC_KEY) as `1`. The key data in this environment variable
is [**Base-85**](https://datatracker.ietf.org/doc/html/rfc1924.html) encoded. The algorithm used is [Elliptic Curve Diffie
Helman](https://en.wikipedia.org/wiki/Elliptic-curve_Diffie–Hellman) with
the [X25519 curve](https://en.wikipedia.org/wiki/Curve25519). A time based
nonce is used to minimise replay attacks. The original JSON command has the
fields: `password` and `timestamp` added. The timestamp is the number of
nanoseconds since the epoch, excluding leap seconds. Commands with a timestamp
more than 5 minutes from the current time are rejected. The command is then
encrypted using AES-256-GCM in authenticated encryption mode, with a symmetric
key that is derived from the ECDH key-pair by running the shared secret through
SHA-256 hashing, once. An IV of at least 96 bits of CSPRNG data is used. The
tag for authenticated encryption **must** be at least 128 bits long. The tag
**must** authenticate only the value of the `encrypted` field. A new command
is created and transmitted that contains the fields:

```
{
    "version": "<kitty version>",
    "iv": "base85 encoded IV",
    "tag": "base85 encoded AEAD tag",
    "pubkey": "base85 encoded ECDH public key of sender",
    "encrypted": "The original command encrypted and base85 encoded"
}
```

## Async and streaming requests[¶](#async-and-streaming-requests "Link to this heading")

Some remote control commands require asynchronous communication, that is, the
response from the terminal can happen after an arbitrary amount of time. For
example, the `select-window` command requires the user to select a window
before a response can be sent. Such command must set the field `async`
in the JSON block above to a random string that serves as a unique id. The
client can cancel an async request in flight by adding the `cancel_async`
field to the JSON block. A async response remains in flight until the terminal
sends a response to the request. Note that cancellation requests dont need to
be encrypted as users must not be prompted for these and the worst a malicious
cancellation request can do is prevent another sync request from getting a
response.

Similar to async requests are *streaming* requests. In these the client has to
send a large amount of data to the terminal and so the request is split into
chunks. In every chunk the JSON block must contain the field `stream` set to
`true` and `stream_id` set to a random long string, that should be the same for
all chunks in a request. End of data is indicated by sending a chunk with no data.

## action[¶](#action "Link to this heading")

Fields are:

`action (required)`
:   The action to perform. Of the form: action [optional args…]

`match_window (optional)`
:   Window to run the action on

`self (default: False)`
:   Whether to use the window this command is run in as the active window

## close-tab[¶](#close-tab "Link to this heading")

Fields are:

`match (default: None)`
:   Which tab to close

`self (default: False)`
:   Boolean indicating whether to close the tab of the window the command is run in

`ignore_no_match (default: False)`
:   Boolean indicating whether no matches should be ignored or return an error

## close-window[¶](#close-window "Link to this heading")

Fields are:

`match (default: None)`
:   Which window to close

`self (default: False)`
:   Boolean indicating whether to close the window the command is run in

`ignore_no_match (default: False)`
:   Boolean indicating whether no matches should be ignored or return an error

## create-marker[¶](#create-marker "Link to this heading")

Fields are:

`match (default: None)`
:   Which window to create the marker in

`self (default: False)`
:   Boolean indicating whether to create marker in the window the command is run in

`marker_spec (optional)`
:   A list or arguments that define the marker specification, for example: [‘text’, ‘1’, ‘ERROR’]

## detach-tab[¶](#detach-tab "Link to this heading")

Fields are:

`match (default: None)`
:   Which tab to detach

`target_tab (default: None)`
:   Which tab to move the detached tab to the OS window it is run in

`self (default: False)`
:   Boolean indicating whether to detach the tab the command is run in

## detach-window[¶](#detach-window "Link to this heading")

Fields are:

`match (default: None)`
:   Which window to detach

`target_tab (default: None)`
:   Which tab to move the detached window to

`self (default: False)`
:   Boolean indicating whether to detach the window the command is run in

`stay_in_tab (default: False)`
:   Boolean indicating focus should remain in the active tab after windows are moved

## disable-ligatures[¶](#disable-ligatures "Link to this heading")

Fields are:

`strategy (required)`
:   One of `never`, `always` or `cursor`

`match_window (optional)`
:   Window to change opacity in

`match_tab (default: None)`
:   Tab to change opacity in

`all (default: False)`
:   Boolean indicating operate on all windows

## env[¶](#env "Link to this heading")

Fields are:

`env (required)`
:   Dictionary of environment variables to values. When a env var ends with = it is removed from the environment.

## focus-tab[¶](#focus-tab "Link to this heading")

Fields are:

`match (default: None)`
:   The tab to focus

## focus-window[¶](#focus-window "Link to this heading")

Fields are:

`match (default: None)`
:   The window to focus

## get-colors[¶](#get-colors "Link to this heading")

Fields are:

`match (default: None)`
:   The window to get the colors for

`configured (default: False)`
:   Boolean indicating whether to get configured or current colors

## get-text[¶](#get-text "Link to this heading")

Fields are:

`match (default: None)`
:   The window to get text from

`extent (default: screen)`
:   One of `screen`, `first_cmd_output_on_screen`, `last_cmd_output`, `last_visited_cmd_output`, `all`, or `selection`

`ansi (default: False)`
:   Boolean, if True send ANSI formatting codes

`cursor (optional)`
:   Boolean, if True send cursor position/style as ANSI codes

`wrap_markers (optional)`
:   Boolean, if True add wrap markers to output

`clear_selection (default: False)`
:   Boolean, if True clear the selection in the matched window

`self (default: False)`
:   Boolean, if True use window the command was run in

## goto-layout[¶](#goto-layout "Link to this heading")

Fields are:

`layout (required)`
:   The new layout name

`match (default: None)`
:   Which tab to change the layout of

## kitten[¶](#kitten "Link to this heading")

Fields are:

`kitten (required)`
:   The name of the kitten to run

`args (optional)`
:   Arguments to pass to the kitten as a list

`match (default: None)`
:   The window to run the kitten over

## last-used-layout[¶](#last-used-layout "Link to this heading")

Fields are:

`match (default: None)`
:   Which tab to change the layout of

`all (default: False)`
:   Boolean to match all tabs

## launch[¶](#launch "Link to this heading")

Fields are:

`args (required)`
:   The command line to run in the new window, as a list, use an empty list to run the default shell

`match (default: None)`
:   The tab to open the new window in

`next_to (default: None)`
:   The window next to which to create the new window or empty string to use active window

`source_window (default: None)`
:   The window to use as source for data or empty string to use active window

`window_title (default: None)`
:   Title for the new window

`cwd (default: None)`
:   Working directory for the new window

`add_to_session (default: None)`
:   Session name to add created window/tab to

`env (default: [])`
:   List of environment variables of the form NAME=VALUE

`var (default: [])`
:   List of user variables of the form NAME=VALUE

`os_panel (default: [])`
:   List of panel settings

`tab_title (default: None)`
:   Title for the new tab

`type (default: window)`
:   The type of window to open

`keep_focus (default: False)`
:   Boolean indicating whether the current window should retain focus or not

`copy_colors (default: False)`
:   Boolean indicating whether to copy the colors from the current window

`copy_cmdline (default: False)`
:   Boolean indicating whether to copy the cmdline from the current window

`copy_env (default: False)`
:   List of strings representing the local env vars

`hold (default: False)`
:   Boolean indicating whether to keep window open after cmd exits

`location (default: default)`
:   Where in the tab to open the new window

`allow_remote_control (default: False)`
:   Boolean indicating whether to allow remote control from the new window

`remote_control_password (default: [])`
:   A list of remote control passwords

`stdin_source (default: none)`
:   Where to get stdin for the process from

`stdin_add_formatting (default: False)`
:   Boolean indicating whether to add formatting codes to stdin

`stdin_add_line_wrap_markers (default: False)`
:   Boolean indicating whether to add line wrap markers to stdin

`spacing (default: [])`
:   A list of spacing specifications, see the docs for the set-spacing command

`marker (default: None)`
:   Specification for marker for new window, for example: “text 1 ERROR”

`logo (default: None)`
:   Path to window logo

`logo_position (default: None)`
:   Window logo position as string or empty string to use default

`logo_alpha (default: -1.0)`
:   Window logo alpha or -1 to use default

`self (default: False)`
:   Boolean, if True use tab the command was run in

`os_window_title (default: None)`
:   Title for OS Window

`os_window_name (default: None)`
:   WM\_NAME for OS Window

`os_window_class (default: None)`
:   WM\_CLASS for OS Window

`os_window_state (default: normal)`
:   The initial state for OS Window

`color (default: [])`
:   list of color specifications such as foreground=red

`watcher (default: [])`
:   list of paths to watcher files

`bias (default: 0.0)`
:   The bias with which to create the new window in the current layout

`wait_for_child_to_exit (default: False)`
:   Boolean indicating whether to wait and return child exit code

`hold_after_ssh (default: False)`
:   Boolean indicating whether to run a local shell after exiting the ssh session cloned via cwd=current or similar

## load-config[¶](#load-config "Link to this heading")

Fields are:

`paths (optional)`
:   List of config file paths to load

`override (default: [])`
:   List of individual config overrides

`ignore_overrides (default: False)`
:   Whether to apply previous overrides

## ls[¶](#ls "Link to this heading")

Fields are:

`all_env_vars (default: False)`
:   Whether to send all environment variables for every window rather than just differing ones

`match (default: None)`
:   Window to change colors in

`match_tab (default: None)`
:   Tab to change colors in

`self (default: False)`
:   Boolean indicating whether to list only the window the command is run in

`output_format (default: json)`
:   Output in json or session format

## new-window[¶](#new-window "Link to this heading")

Fields are:

`args (required)`
:   The command line to run in the new window, as a list, use an empty list to run the default shell

`match (default: None)`
:   The tab to open the new window in

`title (default: None)`
:   Title for the new window

`cwd (default: None)`
:   Working directory for the new window

`keep_focus (default: False)`
:   Boolean indicating whether the current window should retain focus or not

`window_type (default: kitty)`
:   One of `kitty` or `os`

`new_tab (default: False)`
:   Boolean indicating whether to open a new tab

`tab_title (default: None)`
:   Title for the new tab

## remove-marker[¶](#remove-marker "Link to this heading")

Fields are:

`match (default: None)`
:   Which window to remove the marker from

`self (default: False)`
:   Boolean indicating whether to detach the window the command is run in

## resize-os-window[¶](#resize-os-window "Link to this heading")

Fields are:

`match (default: None)`
:   Which window to resize

`self (default: False)`
:   Boolean indicating whether to close the window the command is run in

`incremental (default: False)`
:   Boolean indicating whether to adjust the size incrementally

`action (default: resize)`
:   The action to perform

`unit (default: cells)`
:   One of `cells` or `pixels`

`width (default: 0)`
:   Integer indicating desired window width

`height (default: 0)`
:   Integer indicating desired window height

`os_panel (optional)`
:   Settings for modifying the OS Panel

## resize-window[¶](#resize-window "Link to this heading")

Fields are:

`match (default: None)`
:   Which window to resize

`self (default: False)`
:   Boolean indicating whether to resize the window the command is run in

`increment (default: 2)`
:   Integer specifying the resize increment

`axis (default: horizontal)`
:   One of `horizontal, vertical` or `reset`

## run[¶](#run "Link to this heading")

Fields are:

`data (required)`
:   Chunk of STDIN data, base64 encoded no more than 4096 bytes. Must send an empty chunk to indicate end of data.

`cmdline (required)`
:   The command line to run

`env (default: [])`
:   List of environment variables of the form NAME=VALUE

`allow_remote_control (default: False)`
:   A boolean indicating whether to allow remote control

`remote_control_password (default: [])`
:   A list of remote control passwords

## scroll-window[¶](#scroll-window "Link to this heading")

> for unscrolling by lines, or ‘r’ for scrolling ot prompt.

Fields are:

`amount (required)`
:   The amount to scroll, a two item list with the first item being either a number or the keywords, start and end. And the second item being either ‘p’ for pages or ‘l’ for lines or ‘u’

`match (default: None)`
:   The window to scroll

## select-window[¶](#select-window "Link to this heading")

Fields are:

`match (default: None)`
:   The tab to open the new window in

`self (default: False)`
:   Boolean, if True use tab the command was run in

`title (default: None)`
:   A title for this selection

`exclude_active (default: False)`
:   Exclude the currently active window from the list to pick

`reactivate_prev_tab (default: False)`
:   Reactivate the previously activated tab when finished

## send-key[¶](#send-key "Link to this heading")

Fields are:

`keys (required)`
:   The keys to send

`match (default: None)`
:   A string indicating the window to send text to

`match_tab (default: None)`
:   A string indicating the tab to send text to

`all (default: False)`
:   A boolean indicating all windows should be matched.

`exclude_active (default: False)`
:   A boolean that prevents sending text to the active window

## send-text[¶](#send-text "Link to this heading")

Fields are:

`data (required)`
:   The data being sent. Can be either: text: followed by text or base64: followed by standard base64 encoded bytes

`match (default: None)`
:   A string indicating the window to send text to

`match_tab (default: None)`
:   A string indicating the tab to send text to

`all (default: False)`
:   A boolean indicating all windows should be matched.

`exclude_active (default: False)`
:   A boolean that prevents sending text to the active window

`session_id (optional)`
:   A string that identifies a “broadcast session”

`bracketed_paste (default: disable)`
:   Whether to wrap the text in bracketed paste escape codes

## set-background-image[¶](#set-background-image "Link to this heading")

Fields are:

`data (required)`
:   Chunk of at most 512 bytes of PNG data, base64 encoded. Must send an empty chunk to indicate end of image. Or the special value - to indicate image must be removed.

`match (default: None)`
:   Window to change opacity in

`layout (default: configured)`
:   The image layout

`all (default: False)`
:   Boolean indicating operate on all windows

`configured (default: False)`
:   Boolean indicating if the configured value should be changed

## set-background-opacity[¶](#set-background-opacity "Link to this heading")

Fields are:

`opacity (required)`
:   A number between 0 and 1

`match_window (optional)`
:   Window to change opacity in

`match_tab (default: None)`
:   Tab to change opacity in

`all (default: False)`
:   Boolean indicating operate on all windows

`toggle (default: False)`
:   Boolean indicating if opacity should be toggled between the default and the specified value

## set-colors[¶](#set-colors "Link to this heading")

Fields are:

`colors (required)`
:   An object mapping names to colors as 24-bit RGB integers or null for nullable colors. Or a string for transparent\_background\_colors.

`match_window (optional)`
:   Window to change colors in

`match_tab (default: None)`
:   Tab to change colors in

`all (default: False)`
:   Boolean indicating change colors everywhere or not

`configured (default: False)`
:   Boolean indicating whether to change the configured colors. Must be True if reset is True

`reset (default: False)`
:   Boolean indicating colors should be reset to startup values

## set-enabled-layouts[¶](#set-enabled-layouts "Link to this heading")

Fields are:

`layouts (required)`
:   The list of layout names

`match (default: None)`
:   Which tab to change the layout of

`configured (default: False)`
:   Boolean indicating whether to change the configured value

## set-font-size[¶](#set-font-size "Link to this heading")

Fields are:

`size (required)`
:   The new font size in pts (a positive number). If absent is assumed to be zero which means reset to default.

`all (default: False)`
:   Boolean whether to change font size in the current window or all windows

`increment_op (optional)`
:   The string `+`, `-`, `*` or `/` to interpret size as an increment

## set-spacing[¶](#set-spacing "Link to this heading")

Fields are:

`settings (required)`
:   An object mapping margins/paddings using canonical form {‘margin-top’: 50, ‘padding-left’: null} etc

`match_window (optional)`
:   Window to change paddings and margins in

`match_tab (default: None)`
:   Tab to change paddings and margins in

`all (default: False)`
:   Boolean indicating change paddings and margins everywhere or not

`configured (default: False)`
:   Boolean indicating whether to change the configured paddings and margins. Must be True if reset is True

## set-tab-color[¶](#set-tab-color "Link to this heading")

Fields are:

`colors (required)`
:   An object mapping names to colors as 24-bit RGB integers. A color value of null indicates it should be unset.

`match (default: None)`
:   Which tab to change the color of

`self (default: False)`
:   Boolean indicating whether to use the tab of the window the command is run in

## set-tab-title[¶](#set-tab-title "Link to this heading")

Fields are:

`title (required)`
:   The new title

`match (default: None)`
:   Which tab to change the title of

## set-user-vars[¶](#set-user-vars "Link to this heading")

Fields are:

`var (optional)`
:   List of user variables of the form NAME=VALUE

`match (default: None)`
:   Which windows to change the title in

## set-window-logo[¶](#set-window-logo "Link to this heading")

Fields are:

`data (required)`
:   Chunk of PNG data, base64 encoded no more than 2048 bytes. Must send an empty chunk to indicate end of image. Or the special value `-` to indicate image must be removed.

`position (default: None)`
:   The logo position as a string, empty string means default

`alpha (default: -1.0)`
:   The logo alpha between `0` and `1`. `-1` means use default

`match (default: None)`
:   Which window to change the logo in

`self (default: False)`
:   Boolean indicating whether to act on the window the command is run in

## set-window-title[¶](#set-window-title "Link to this heading")

Fields are:

`title (optional)`
:   The new title

`match (default: None)`
:   Which windows to change the title in

`temporary (default: False)`
:   Boolean indicating if the change is temporary or permanent

## signal-child[¶](#signal-child "Link to this heading")

Fields are:

`signals (required)`
:   The signals, a list of names, such as `SIGTERM`, `SIGKILL`, `SIGUSR1`, etc.

`match (default: None)`
:   Which windows to send the signals to
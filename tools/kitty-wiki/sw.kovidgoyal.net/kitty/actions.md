---
source_url: "https://sw.kovidgoyal.net/kitty/actions/"
title: "Mappable actions - kitty"
crawl_date: "2025-11-16T14:48:10.132761Z"
selector: "article"
---

# Mappable actions - kitty

# Mappable actions[¶](#mappable-actions "Link to this heading")

The actions described below can be mapped to any key press or mouse action
using the `map` and `mouse_map` directives in `kitty.conf`. For
configuration examples, see the default shortcut links for each action.
To read about keyboard mapping in more detail, see [Making your keyboard dance](../mapping/).

# Copy/paste[¶](#copy-paste "Link to this heading")

clear\_selection[¶](#action-clear_selection "Link to this definition")

Clear the current selection

copy\_and\_clear\_or\_interrupt[¶](#action-copy_and_clear_or_interrupt "Link to this definition")

Copy the selected text from the active window to the clipboard and clear selection, if no selection, send SIGINT (aka `ctrl`+`c`)

copy\_ansi\_to\_clipboard[¶](#action-copy_ansi_to_clipboard "Link to this definition")

Copy the selected text from the active window to the clipboard with ANSI formatting codes

copy\_or\_interrupt[¶](#action-copy_or_interrupt "Link to this definition")

Copy the selected text from the active window to the clipboard, if no selection, send SIGINT (aka `ctrl`+`c`)

copy\_or\_noop[¶](#action-copy_or_noop "Link to this definition")

Copy the selected text from the active window to the clipboard, if no selection, pass the key through to the application running in the terminal.

Default shortcuts using this action:
[`cmd+c`](../conf/#shortcut-kitty.Copy-to-clipboard-or-pass-through)

copy\_to\_clipboard[¶](#action-copy_to_clipboard "Link to this definition")

Copy the selected text from the active window to the clipboard

Default shortcuts using this action:
[`ctrl+shift+c`](../conf/#shortcut-kitty.Copy-to-clipboard)

pass\_selection\_to\_program[¶](#action-pass_selection_to_program "Link to this definition")

Pass the selected text from the active window to the specified program

Default shortcuts using this action:
[`ctrl+shift+o`](../conf/#shortcut-kitty.Pass-selection-to-program)

paste[¶](#action-paste "Link to this definition")

Paste the specified text into the current window. ANSI C escapes are decoded.

show\_first\_command\_output\_on\_screen[¶](#action-show_first_command_output_on_screen "Link to this definition")

Show output from the first shell command on screen in a pager like less

Requires [Shell integration](../shell-integration/#shell-integration) to work

show\_last\_command\_output[¶](#action-show_last_command_output "Link to this definition")

Show output from the last shell command in a pager like less

Requires [Shell integration](../shell-integration/#shell-integration) to work

Default shortcuts using this action:
[`ctrl+shift+g`](../conf/#shortcut-kitty.Browse-output-of-the-last-shell-command-in-pager)

show\_last\_non\_empty\_command\_output[¶](#action-show_last_non_empty_command_output "Link to this definition")

Show the last non-empty output from a shell command in a pager like less

Requires [Shell integration](../shell-integration/#shell-integration) to work

show\_last\_visited\_command\_output[¶](#action-show_last_visited_command_output "Link to this definition")

Show the first command output below the last scrolled position via scroll\_to\_prompt

or the last mouse clicked command output in a pager like less

Requires [Shell integration](../shell-integration/#shell-integration) to work

show\_scrollback[¶](#action-show_scrollback "Link to this definition")

Show scrollback in a pager like less

Default shortcuts using this action:
[`ctrl+shift+h`](../conf/#shortcut-kitty.Browse-scrollback-buffer-in-pager)

copy\_to\_buffer[¶](#action-copy_to_buffer "Link to this definition")

Copy the selection from the active window to the specified buffer

See [Multiple copy/paste buffers](../overview/#cpbuf) for details.

paste\_from\_buffer[¶](#action-paste_from_buffer "Link to this definition")

Paste from the specified buffer to the active window

See [Multiple copy/paste buffers](../overview/#cpbuf) for details.

paste\_from\_clipboard[¶](#action-paste_from_clipboard "Link to this definition")

Paste from the clipboard to the active window

Default shortcuts using this action:
[`ctrl+shift+v`](../conf/#shortcut-kitty.Paste-from-clipboard)

paste\_from\_selection[¶](#action-paste_from_selection "Link to this definition")

Paste from the primary selection, if present, otherwise the clipboard to the active window

Default shortcuts using this action:
[`ctrl+shift+s`](../conf/#shortcut-kitty.Paste-from-selection)

# Debugging[¶](#debugging "Link to this heading")

dump\_lines\_with\_attrs[¶](#action-dump_lines_with_attrs "Link to this definition")

Show a dump of the current lines in the scrollback + screen with their line attributes

close\_shared\_ssh\_connections[¶](#action-close_shared_ssh_connections "Link to this definition")

Close all shared SSH connections

See [`share_connections`](../kittens/ssh/#opt-kitten-ssh.share_connections) for details.

debug\_config[¶](#action-debug_config "Link to this definition")

Show the effective configuration kitty is running with

Default shortcuts using this action:
[`ctrl+shift+f6`](../conf/#shortcut-kitty.Debug-kitty-configuration)

show\_kitty\_env\_vars[¶](#action-show_kitty_env_vars "Link to this definition")

Show the environment variables that the kitty process sees

simulate\_color\_scheme\_preference\_change[¶](#action-simulate_color_scheme_preference_change "Link to this definition")

Simulate a change in OS color scheme preference

# Layouts[¶](#layouts "Link to this heading")

goto\_layout[¶](#action-goto_layout "Link to this definition")

Switch to the named layout

In case there are multiple layouts with the same name and different options,
specify the full layout definition or a unique prefix of the full definition.

For example:

```
map f1 goto_layout tall
map f2 goto_layout fat:bias=20
```

last\_used\_layout[¶](#action-last_used_layout "Link to this definition")

Go to the previously used layout

layout\_action[¶](#action-layout_action "Link to this definition")

Perform a layout specific action. See [Arrange windows](../layouts/) for details

next\_layout[¶](#action-next_layout "Link to this definition")

Go to the next enabled layout. Can optionally supply an integer to jump by the specified number.

Default shortcuts using this action:
[`ctrl+shift+l`](../conf/#shortcut-kitty.Next-layout)

toggle\_layout[¶](#action-toggle_layout "Link to this definition")

Toggle the named layout

Switches to the named layout if another layout is current, otherwise
switches to the last used layout. Useful to “zoom” a window temporarily
by switching to the stack layout. See also [`scrollback_fill_enlarged_window`](../conf/#opt-kitty.scrollback_fill_enlarged_window)
if you would like content from the scrollback buffer to scroll down into the
zoomed window. For example:

```
map f1 toggle_layout stack
```

# Marks[¶](#marks "Link to this heading")

remove\_marker[¶](#action-remove_marker "Link to this definition")

Remove a previously created marker

scroll\_to\_mark[¶](#action-scroll_to_mark "Link to this definition")

Scroll to the next or previous mark of the specified type

toggle\_marker[¶](#action-toggle_marker "Link to this definition")

Toggle the current marker on/off

create\_marker[¶](#action-create_marker "Link to this definition")

Create a new marker

# Miscellaneous[¶](#miscellaneous "Link to this heading")

send\_key[¶](#action-send_key "Link to this definition")

Send the specified keys to the active window.

Note that the key will be sent only if the current keyboard mode of the program running in the terminal supports it.
Both key press and key release are sent. First presses for all specified keys and then releases in reverse order.
To send a pattern of press and release for multiple keys use the [`combine`](#action-combine) action. For example:

```
map f1 send_key ctrl+x alt+y
map f1 combine : send_key ctrl+x : send_key alt+y
```

send\_text[¶](#action-send_text "Link to this definition")

Send the specified text to the active window

See [`send_text`](../conf/#shortcut-kitty.Send-arbitrary-text-on-key-presses) for details.

Default shortcuts using this action:
[`ctrl+shift+alt+h`](../conf/#shortcut-kitty.Send-arbitrary-text-on-key-presses)

show\_kitty\_doc[¶](#action-show_kitty_doc "Link to this definition")

Display the specified kitty documentation, preferring a local copy, if found.

For example:

```
# show the config docs
map f1 show_kitty_doc conf
# show the ssh kitten docs
map f1 show_kitty_doc kittens/ssh
```

Default shortcuts using this action:
[`ctrl+shift+f1`](../conf/#shortcut-kitty.Show-documentation)

signal\_child[¶](#action-signal_child "Link to this definition")

Send the specified SIGNAL to the foreground process in the active window

For example:

```
map f1 signal_child SIGTERM
```

clear\_terminal[¶](#action-clear_terminal "Link to this definition")

Clear the terminal

See [`reset_terminal`](../conf/#shortcut-kitty.Reset-the-terminal) for details. For example:

```
# Reset the terminal
map f1 clear_terminal reset active
# Clear the terminal screen by erasing all contents
map f1 clear_terminal clear active
# Clear the terminal scrollback by erasing it
map f1 clear_terminal scrollback active
# Scroll the contents of the screen into the scrollback
map f1 clear_terminal scroll active
# Clear everything on screen up to the line with the cursor or the start of the current prompt (needs shell integration)
# Useful for clearing the screen up to the shell prompt and moving the shell prompt to the top of the screen.
map f1 clear_terminal to_cursor active
# Same as above except cleared lines are moved into scrollback
map f1 clear_terminal to_cursor_scroll active
# Erase the last command and its output (needs shell integration to work)
map f1 clear_terminal last_command active
```

Default shortcuts using this action:
[`cmd+l`](../conf/#shortcut-kitty.Clear-the-last-command), [`cmd+ctrl+l`](../conf/#shortcut-kitty.Clear-screen), [`option+cmd+k`](../conf/#shortcut-kitty.Clear-scrollback), [`cmd+k`](../conf/#shortcut-kitty.Clear-to-start), [`ctrl+shift+delete`](../conf/#shortcut-kitty.Reset-the-terminal)

combine[¶](#action-combine "Link to this definition")

Combine multiple actions and map to a single keypress

The syntax is:

```
map key combine <separator> action1 <separator> action2 <separator> action3 ...
```

For example:

```
map kitty_mod+e combine : new_window : next_layout
map kitty_mod+e combine | new_tab | goto_tab -1
```

disable\_ligatures\_in[¶](#action-disable_ligatures_in "Link to this definition")

Turn on/off ligatures in the specified window

See [`disable_ligatures`](../conf/#opt-kitty.disable_ligatures) for details

discard\_event[¶](#action-discard_event "Link to this definition")

Discard this event completely ignoring it

edit\_config\_file[¶](#action-edit_config_file "Link to this definition")

Edit the kitty.conf config file in your favorite text editor

Default shortcuts using this action:
[`ctrl+shift+f2`](../conf/#shortcut-kitty.Edit-config-file)

grab\_keyboard[¶](#action-grab_keyboard "Link to this definition")

Grab the keyboard. This means global shortcuts defined in the OS will be passed to kitty instead. Useful if

you want to create an OS modal window. How well this
works depends on the OS/window manager/desktop environment. On Wayland it works only if the compositor implements
the [inhibit-keyboard-shortcuts protocol](https://wayland.app/protocols/keyboard-shortcuts-inhibit-unstable-v1).
On macOS Apple doesn’t allow applications to grab the keyboard without special permissions, so it doesn’t work.

hide\_macos\_app[¶](#action-hide_macos_app "Link to this definition")

Hide macOS kitty application

Default shortcuts using this action:
[`cmd+h`](../conf/#shortcut-kitty.Hide-macOS-kitty-application)

hide\_macos\_other\_apps[¶](#action-hide_macos_other_apps "Link to this definition")

Hide macOS other applications

Default shortcuts using this action:
[`opt+cmd+h`](../conf/#shortcut-kitty.Hide-macOS-other-applications)

input\_unicode\_character[¶](#action-input_unicode_character "Link to this definition")

Input an arbitrary unicode character. See [Unicode input](../kittens/unicode_input/) for details.

kitten[¶](#action-kitten "Link to this definition")

Run the specified kitten. See [Custom kittens](../kittens/custom/) for details

Default shortcuts using this action:

* [Hints](../kittens/hints/) - [`ctrl+shift+p>h`](../conf/#shortcut-kitty.Insert-selected-hash) Insert selected hash
* [Hints](../kittens/hints/) - [`ctrl+shift+p>l`](../conf/#shortcut-kitty.Insert-selected-line) Insert selected line
* [Hints](../kittens/hints/) - [`ctrl+shift+p>f`](../conf/#shortcut-kitty.Insert-selected-path) Insert selected path
* [Hints](../kittens/hints/) - [`ctrl+shift+p>w`](../conf/#shortcut-kitty.Insert-selected-word) Insert selected word
* [Hints](../kittens/hints/) - [`ctrl+shift+p>shift+f`](../conf/#shortcut-kitty.Open-selected-path) Open selected path
* [Hints](../kittens/hints/) - [`ctrl+shift+p>n`](../conf/#shortcut-kitty.Open-the-selected-file-at-the-selected-line) Open the selected file at the selected line
* [Hints](../kittens/hints/) - [`ctrl+shift+p>y`](../conf/#shortcut-kitty.Open-the-selected-hyperlink) Open the selected hyperlink
* [Unicode input](../kittens/unicode_input/) - [`ctrl+shift+u`](../conf/#shortcut-kitty.Unicode-input) Unicode input

kitty\_shell[¶](#action-kitty_shell "Link to this definition")

Run the kitty shell to control kitty with commands

Default shortcuts using this action:
[`ctrl+shift+escape`](../conf/#shortcut-kitty.Open-the-kitty-command-shell)

launch[¶](#action-launch "Link to this definition")

Launch the specified program in a new window/tab/etc.

See [The launch command](../launch/) for details

load\_config\_file[¶](#action-load_config_file "Link to this definition")

Reload the config file

If mapped without arguments reloads the default config file, otherwise loads
the specified config files, in order. Loading a config file *replaces* all
config options. For example:

```
map f5 load_config_file /path/to/some/kitty.conf
```

Default shortcuts using this action:
[`ctrl+shift+f5`](../conf/#shortcut-kitty.Reload-kitty.conf)

macos\_cycle\_through\_os\_windows[¶](#action-macos_cycle_through_os_windows "Link to this definition")

Cycle through OS windows on macOS

Default shortcuts using this action:
[`` cmd+` ``](../conf/#shortcut-kitty.macOS-Cycle-through-OS-Windows)

minimize\_macos\_window[¶](#action-minimize_macos_window "Link to this definition")

Minimize macOS window

Default shortcuts using this action:
[`cmd+m`](../conf/#shortcut-kitty.Minimize-macOS-window)

open\_url[¶](#action-open_url "Link to this definition")

Open the specified URL

Default shortcuts using this action:
[`shift+cmd+/`](../conf/#shortcut-kitty.Open-kitty-Website)

open\_url\_with\_hints[¶](#action-open_url_with_hints "Link to this definition")

Click a URL using the keyboard

Default shortcuts using this action:
[`ctrl+shift+e`](../conf/#shortcut-kitty.Open-URL)

pop\_keyboard\_mode[¶](#action-pop_keyboard_mode "Link to this definition")

End the current keyboard mode switching to the previous mode.

push\_keyboard\_mode[¶](#action-push_keyboard_mode "Link to this definition")

Switch to the specified keyboard mode, pushing it onto the stack of keyboard modes.

remote\_control[¶](#action-remote_control "Link to this definition")

Run a remote control command without needing to allow remote control

For example:

```
map f1 remote_control set-spacing margin=30
```

See [Mapping key presses to remote control commands](../remote-control/#rc-mapping) for details.

remote\_control\_script[¶](#action-remote_control_script "Link to this definition")

Run a remote control script without needing to allow remote control

For example:

```
map f1 remote_control_script /path/to/script arg1 arg2 ...
```

See [Mapping key presses to remote control commands](../remote-control/#rc-mapping) for details.

set\_colors[¶](#action-set_colors "Link to this definition")

Change colors in the specified windows

For details, see [kitten @ set-colors](../remote-control/#at-set-colors). For example:

```
map f5 set_colors --configured /path/to/some/config/file/colors.conf
```

show\_error[¶](#action-show_error "Link to this definition")

Show an error message with the specified title and text

sleep[¶](#action-sleep "Link to this definition")

Sleep for the specified time period. Suffix can be s for seconds, m, for minutes, h for hours and d for days. The time can be fractional.

toggle\_macos\_secure\_keyboard\_entry[¶](#action-toggle_macos_secure_keyboard_entry "Link to this definition")

Toggle macOS secure keyboard entry

Default shortcuts using this action:
[`opt+cmd+s`](../conf/#shortcut-kitty.Toggle-macOS-secure-keyboard-entry)

ungrab\_keyboard[¶](#action-ungrab_keyboard "Link to this definition")

Ungrab the keyboard if it was previously grabbed

no\_op[¶](#action-no_op "Link to this definition")

Unbind a shortcut

Mapping a shortcut to no\_op causes kitty to not intercept the key stroke anymore, instead passing it to the program running inside it.

# Mouse actions[¶](#mouse-actions "Link to this heading")

mouse\_click\_url[¶](#action-mouse_click_url "Link to this definition")

Click the URL under the mouse

mouse\_click\_url\_or\_select[¶](#action-mouse_click_url_or_select "Link to this definition")

Click the URL under the mouse only if the screen has no selection

mouse\_handle\_click[¶](#action-mouse_handle_click "Link to this definition")

Handle a mouse click

Try to perform the specified actions one after the other till one of them is successful.
Supported actions are:

```
selection - check for a selection and if one exists abort processing
link - if a link exists under the mouse, click it
prompt - if the mouse click happens at a shell prompt move the cursor to the mouse location
```

For examples, see [Mouse actions](../conf/#conf-kitty-mouse-mousemap)

mouse\_select\_command\_output[¶](#action-mouse_select_command_output "Link to this definition")

Select clicked command output

Requires [Shell integration](../shell-integration/#shell-integration) to work

mouse\_selection[¶](#action-mouse_selection "Link to this definition")

Manipulate the selection based on the current mouse position

For examples, see [Mouse actions](../conf/#conf-kitty-mouse-mousemap)

mouse\_show\_command\_output[¶](#action-mouse_show_command_output "Link to this definition")

Show clicked command output in a pager like less

Requires [Shell integration](../shell-integration/#shell-integration) to work

paste\_selection[¶](#action-paste_selection "Link to this definition")

Paste the current primary selection

paste\_selection\_or\_clipboard[¶](#action-paste_selection_or_clipboard "Link to this definition")

Paste the current primary selection or the clipboard if no selection is present

# Scrolling[¶](#scrolling "Link to this heading")

scroll\_end[¶](#action-scroll_end "Link to this definition")

Scroll to the bottom of the scrollback buffer when in main screen

Default shortcuts using this action:
[`ctrl+shift+end`](../conf/#shortcut-kitty.Scroll-to-bottom)

scroll\_home[¶](#action-scroll_home "Link to this definition")

Scroll to the top of the scrollback buffer when in main screen

Default shortcuts using this action:
[`ctrl+shift+home`](../conf/#shortcut-kitty.Scroll-to-top)

scroll\_line\_down[¶](#action-scroll_line_down "Link to this definition")

Scroll down by one line when in main screen. To scroll by different amounts, you can map the remote\_control scroll-window action.

Default shortcuts using this action:
[`ctrl+shift+down`](../conf/#shortcut-kitty.Scroll-line-down)

scroll\_line\_up[¶](#action-scroll_line_up "Link to this definition")

Scroll up by one line when in main screen. To scroll by different amounts, you can map the remote\_control scroll-window action.

Default shortcuts using this action:
[`ctrl+shift+up`](../conf/#shortcut-kitty.Scroll-line-up)

scroll\_page\_down[¶](#action-scroll_page_down "Link to this definition")

Scroll down by one page when in main screen. To scroll by different amounts, you can map the remote\_control scroll-window action.

Default shortcuts using this action:
[`ctrl+shift+page_down`](../conf/#shortcut-kitty.Scroll-page-down)

scroll\_page\_up[¶](#action-scroll_page_up "Link to this definition")

Scroll up by one page when in main screen. To scroll by different amounts, you can map the remote\_control scroll-window action.

Default shortcuts using this action:
[`ctrl+shift+page_up`](../conf/#shortcut-kitty.Scroll-page-up)

scroll\_prompt\_to\_bottom[¶](#action-scroll_prompt_to_bottom "Link to this definition")

Scroll prompt to the bottom of the screen, filling in extra lines from the scrollback buffer, when in main screen

scroll\_prompt\_to\_top[¶](#action-scroll_prompt_to_top "Link to this definition")

Scroll prompt to the top of the screen, filling screen with empty lines, when in main screen. To avoid putting the lines above the prompt into the scrollback use scroll\_prompt\_to\_top y

scroll\_to\_prompt[¶](#action-scroll_to_prompt "Link to this definition")

Scroll to the previous/next shell command prompt

Allows easy jumping from one command to the next. Requires working
[Shell integration](../shell-integration/#shell-integration). Takes two optional numbers as arguments:

The first is the number of prompts to jump; negative values jump up and
positive values jump down. A value of zero will jump to the last prompt
visited by this action. Defaults to -1

The second is the number of lines to show above the prompt that was
jumped to. This is somewhat like less’s --jump-target option or
vim’s scrolloff setting. Defaults to 0.

For example:

```
map ctrl+p scroll_to_prompt -1 3  # jump to previous, showing 3 lines prior
map ctrl+n scroll_to_prompt 1     # jump to next
map ctrl+o scroll_to_prompt 0     # jump to last visited
```

Default shortcuts using this action:
[`ctrl+shift+x`](../conf/#shortcut-kitty.Scroll-to-next-shell-prompt), [`ctrl+shift+z`](../conf/#shortcut-kitty.Scroll-to-previous-shell-prompt)

# Sessions[¶](#sessions "Link to this heading")

close\_session[¶](#action-close_session "Link to this definition")

Close a session, that is, close all windows that belong to the session.

Examples::
:   # Ask for the session to close
    map f1 close\_session
    # Close the currently active session
    map f1 close\_session .
    # Close session by name
    map f1 close\_session “my session”
    # Close session by path to session file
    map f1 close\_session “/path/to/session/file.kitty-session”

goto\_session[¶](#action-goto_session "Link to this definition")

Switch to the specified session, creating it if not already present. See [Creating/Switching to sessions with a keypress](../sessions/#goto-session).

save\_as\_session[¶](#action-save_as_session "Link to this definition")

Save the current kitty state as a session file. See [The save\_as\_session action](../sessions/#save-as-session).

# Tab management[¶](#tab-management "Link to this heading")

close\_other\_tabs\_in\_os\_window[¶](#action-close_other_tabs_in_os_window "Link to this definition")

Close all the tabs in the current OS window other than the currently active tab

close\_tab[¶](#action-close_tab "Link to this definition")

Close the current tab

Default shortcuts using this action:
[`ctrl+shift+q`](../conf/#shortcut-kitty.Close-tab)

detach\_tab[¶](#action-detach_tab "Link to this definition")

Detach a tab, moving it to another OS Window

See [detaching windows](../invocation/#detach-window) for details.

goto\_tab[¶](#action-goto_tab "Link to this definition")

Go to the specified tab, by number, starting with 1

Zero and negative numbers go to previously active tabs.
Use the [`select_tab`](#action-select_tab) action to interactively select a tab
to go to.

move\_tab\_backward[¶](#action-move_tab_backward "Link to this definition")

Move the active tab backward

Default shortcuts using this action:
[`ctrl+shift+,`](../conf/#shortcut-kitty.Move-tab-backward)

move\_tab\_forward[¶](#action-move_tab_forward "Link to this definition")

Move the active tab forward

Default shortcuts using this action:
[`ctrl+shift+.`](../conf/#shortcut-kitty.Move-tab-forward)

new\_tab[¶](#action-new_tab "Link to this definition")

Create a new tab

Default shortcuts using this action:
[`ctrl+shift+t`](../conf/#shortcut-kitty.New-tab)

new\_tab\_with\_cwd[¶](#action-new_tab_with_cwd "Link to this definition")

Create a new tab with working directory for the window in it set to the same as the active window.

The tab is added to the currently active [session](../sessions/#sessions), if any.

next\_tab[¶](#action-next_tab "Link to this definition")

Make the next tab active

Default shortcuts using this action:
[`ctrl+shift+right`](../conf/#shortcut-kitty.Next-tab)

previous\_tab[¶](#action-previous_tab "Link to this definition")

Make the previous tab active

Default shortcuts using this action:
[`ctrl+shift+left`](../conf/#shortcut-kitty.Previous-tab)

select\_tab[¶](#action-select_tab "Link to this definition")

Interactively select a tab to switch to

set\_tab\_title[¶](#action-set_tab_title "Link to this definition")

Change the title of the active tab interactively, by typing in the new title.

If you specify an argument to this action then that is used as the title instead of asking for it.
Use the empty string (“”) to reset the title to default. Use a space (” “) to indicate that the
prompt should not be pre-filled. For example:

```
# interactive usage
map f1 set_tab_title
# set a specific title
map f2 set_tab_title some title
# reset to default
map f3 set_tab_title ""
# interactive usage without prefilled prompt
map f3 set_tab_title " "
```

Default shortcuts using this action:
[`ctrl+shift+alt+t`](../conf/#shortcut-kitty.Set-tab-title)

# Window management[¶](#window-management "Link to this heading")

set\_window\_title[¶](#action-set_window_title "Link to this definition")

Change the title of the active window interactively, by typing in the new title.

If you specify an argument to this action then that is used as the title instead of asking for it.
Use the empty string (“”) to reset the title to default. Use a space (” “) to indicate that the
prompt should not be pre-filled. For example:

```
# interactive usage
map f1 set_window_title
# set a specific title
map f2 set_window_title some title
# reset to default
map f3 set_window_title ""
# interactive usage without prefilled prompt
map f3 set_window_title " "
```

close\_other\_windows\_in\_tab[¶](#action-close_other_windows_in_tab "Link to this definition")

Close all windows in the tab other than the currently active window

eighth\_window[¶](#action-eighth_window "Link to this definition")

Focus the eighth window

Default shortcuts using this action:
[`ctrl+shift+8`](../conf/#shortcut-kitty.Eighth-window)

fifth\_window[¶](#action-fifth_window "Link to this definition")

Focus the fifth window

Default shortcuts using this action:
[`ctrl+shift+5`](../conf/#shortcut-kitty.Fifth-window)

first\_window[¶](#action-first_window "Link to this definition")

Focus the first window

Default shortcuts using this action:
[`ctrl+shift+1`](../conf/#shortcut-kitty.First-window)

focus\_visible\_window[¶](#action-focus_visible_window "Link to this definition")

Focus a visible window by pressing the number of the window. Window numbers are displayed

over the windows for easy selection in this mode. See [`visual_window_select_characters`](../conf/#opt-kitty.visual_window_select_characters).

Default shortcuts using this action:
[`ctrl+shift+f7`](../conf/#shortcut-kitty.Visually-select-and-focus-window)

fourth\_window[¶](#action-fourth_window "Link to this definition")

Focus the fourth window

Default shortcuts using this action:
[`ctrl+shift+4`](../conf/#shortcut-kitty.Fourth-window)

move\_window[¶](#action-move_window "Link to this definition")

Move the window in the specified direction

For example:

```
map ctrl+left move_window left
map ctrl+down move_window bottom
```

move\_window\_backward[¶](#action-move_window_backward "Link to this definition")

Move active window backward (swap it with the previous window)

Default shortcuts using this action:
[`ctrl+shift+b`](../conf/#shortcut-kitty.Move-window-backward)

move\_window\_forward[¶](#action-move_window_forward "Link to this definition")

Move active window forward (swap it with the next window)

Default shortcuts using this action:
[`ctrl+shift+f`](../conf/#shortcut-kitty.Move-window-forward)

move\_window\_to\_top[¶](#action-move_window_to_top "Link to this definition")

Move active window to the top (make it the first window)

Default shortcuts using this action:
[`` ctrl+shift+` ``](../conf/#shortcut-kitty.Move-window-to-top)

neighboring\_window[¶](#action-neighboring_window "Link to this definition")

Focus the neighboring window in the current tab

For example:

```
map ctrl+left neighboring_window left
map ctrl+down neighboring_window bottom
```

next\_window[¶](#action-next_window "Link to this definition")

Focus the next window in the current tab

Default shortcuts using this action:
[`ctrl+shift+]`](../conf/#shortcut-kitty.Next-window)

ninth\_window[¶](#action-ninth_window "Link to this definition")

Focus the ninth window

Default shortcuts using this action:
[`ctrl+shift+9`](../conf/#shortcut-kitty.Ninth-window)

nth\_window[¶](#action-nth_window "Link to this definition")

Focus the nth window if positive or the previously active windows if negative. When the number is larger

than the number of windows focus the last window. For example:

```
# focus the previously active window
map ctrl+p nth_window -1
# focus the first window
map ctrl+1 nth_window 0
```

previous\_window[¶](#action-previous_window "Link to this definition")

Focus the previous window in the current tab

Default shortcuts using this action:
[`ctrl+shift+[`](../conf/#shortcut-kitty.Previous-window)

reset\_window\_sizes[¶](#action-reset_window_sizes "Link to this definition")

Reset window sizes undoing any dynamic resizing of windows

resize\_window[¶](#action-resize_window "Link to this definition")

Resize the active window by the specified amount

See [Resizing windows](../layouts/#window-resizing) for details.

second\_window[¶](#action-second_window "Link to this definition")

Focus the second window

Default shortcuts using this action:
[`ctrl+shift+2`](../conf/#shortcut-kitty.Second-window)

seventh\_window[¶](#action-seventh_window "Link to this definition")

Focus the seventh window

Default shortcuts using this action:
[`ctrl+shift+7`](../conf/#shortcut-kitty.Seventh-window)

sixth\_window[¶](#action-sixth_window "Link to this definition")

Focus the sixth window

Default shortcuts using this action:
[`ctrl+shift+6`](../conf/#shortcut-kitty.Sixth-window)

swap\_with\_window[¶](#action-swap_with_window "Link to this definition")

Swap the current window with another window in the current tab, selected visually. See [`visual_window_select_characters`](../conf/#opt-kitty.visual_window_select_characters)

Default shortcuts using this action:
[`ctrl+shift+f8`](../conf/#shortcut-kitty.Visually-swap-window-with-another)

tenth\_window[¶](#action-tenth_window "Link to this definition")

Focus the tenth window

Default shortcuts using this action:
[`ctrl+shift+0`](../conf/#shortcut-kitty.Tenth-window)

third\_window[¶](#action-third_window "Link to this definition")

Focus the third window

Default shortcuts using this action:
[`ctrl+shift+3`](../conf/#shortcut-kitty.Third-window)

change\_font\_size[¶](#action-change_font_size "Link to this definition")

Change the font size for the current or all OS Windows

See [Font sizes](../conf/#conf-kitty-shortcuts-fonts) for details.

Default shortcuts using this action:
[`ctrl+shift+minus`](../conf/#shortcut-kitty.Decrease-font-size), [`ctrl+shift+equal`](../conf/#shortcut-kitty.Increase-font-size), [`ctrl+shift+backspace`](../conf/#shortcut-kitty.Reset-font-size)

close\_os\_window[¶](#action-close_os_window "Link to this definition")

Close the currently active OS Window

Default shortcuts using this action:
[`shift+cmd+w`](../conf/#shortcut-kitty.Close-OS-window)

close\_other\_os\_windows[¶](#action-close_other_os_windows "Link to this definition")

Close all other OS Windows other than the OS Window containing the currently active window

close\_window[¶](#action-close_window "Link to this definition")

Close the currently active window

Default shortcuts using this action:
[`ctrl+shift+w`](../conf/#shortcut-kitty.Close-window)

close\_window\_with\_confirmation[¶](#action-close_window_with_confirmation "Link to this definition")

Close window with confirmation

Asks for confirmation before closing the window. If you don’t want the
confirmation when the window is sitting at a shell prompt
(requires [Shell integration](../shell-integration/#shell-integration)), use:

```
map f1 close_window_with_confirmation ignore-shell
```

detach\_window[¶](#action-detach_window "Link to this definition")

Detach a window, moving it to another tab or OS Window

See [detaching windows](../invocation/#detach-window) for details.

new\_os\_window[¶](#action-new_os_window "Link to this definition")

New OS Window

Default shortcuts using this action:
[`ctrl+shift+n`](../conf/#shortcut-kitty.New-OS-window)

new\_os\_window\_with\_cwd[¶](#action-new_os_window_with_cwd "Link to this definition")

New OS Window with the same working directory as the currently active window.

The new OS Window is added to the currently active [session](../sessions/#sessions), if any.

new\_window[¶](#action-new_window "Link to this definition")

Create a new window

Default shortcuts using this action:
[`ctrl+shift+enter`](../conf/#shortcut-kitty.New-window)

new\_window\_with\_cwd[¶](#action-new_window_with_cwd "Link to this definition")

Create a new window with working directory same as that of the active window.

The new window will belong to the active [session](../sessions/#sessions) if any.

nth\_os\_window[¶](#action-nth_os_window "Link to this definition")

Focus the nth OS window if positive or the previously active OS windows if negative. When the number is larger

than the number of OS windows focus the last OS window. A value of zero will refocus the currently focused OS window,
this is useful if focus is not on any kitty OS window at all, however, it will only work if the window manager
allows applications to grab focus. For example:

```
# focus the previously active kitty OS window
map ctrl+p nth_os_window -1
# focus the current kitty OS window (grab focus)
map ctrl+0 nth_os_window 0
# focus the first kitty OS window
map ctrl+1 nth_os_window 1
# focus the last kitty OS window
map ctrl+1 nth_os_window 999
```

quit[¶](#action-quit "Link to this definition")

Quit, closing all windows

Default shortcuts using this action:
[`cmd+q`](../conf/#shortcut-kitty.Quit-kitty)

set\_background\_opacity[¶](#action-set_background_opacity "Link to this definition")

Set the background opacity for the active OS Window

For example:

```
map f1 set_background_opacity +0.1
map f2 set_background_opacity -0.1
map f3 set_background_opacity 0.5
```

Default shortcuts using this action:
[`ctrl+shift+a>l`](../conf/#shortcut-kitty.Decrease-background-opacity), [`ctrl+shift+a>1`](../conf/#shortcut-kitty.Make-background-fully-opaque), [`ctrl+shift+a>m`](../conf/#shortcut-kitty.Increase-background-opacity), [`ctrl+shift+a>d`](../conf/#shortcut-kitty.Reset-background-opacity)

start\_resizing\_window[¶](#action-start_resizing_window "Link to this definition")

Resize the active window interactively

See [Resizing windows](../layouts/#window-resizing) for details.

Default shortcuts using this action:
[`ctrl+shift+r`](../conf/#shortcut-kitty.Start-resizing-window)

toggle\_fullscreen[¶](#action-toggle_fullscreen "Link to this definition")

Toggle the fullscreen status of the active OS Window

Default shortcuts using this action:
[`ctrl+shift+f11`](../conf/#shortcut-kitty.Toggle-fullscreen)

toggle\_maximized[¶](#action-toggle_maximized "Link to this definition")

Toggle the maximized status of the active OS Window

Default shortcuts using this action:
[`ctrl+shift+f10`](../conf/#shortcut-kitty.Toggle-maximized)

toggle\_tab[¶](#action-toggle_tab "Link to this definition")

Toggle to the tab matching the specified expression

Switches to the matching tab if another tab is current, otherwise
switches to the last used tab. Useful to easily switch to and back from a
tab using a single shortcut. Note that toggling works only between
tabs in the same OS window. See [Matching windows and tabs](../remote-control/#search-syntax) for details
on the match expression. For example:

```
map f1 toggle_tab title:mytab
```
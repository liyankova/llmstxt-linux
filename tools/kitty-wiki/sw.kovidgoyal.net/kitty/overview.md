---
source_url: "https://sw.kovidgoyal.net/kitty/overview/"
title: "Overview - kitty"
crawl_date: "2025-11-16T14:47:57.321938Z"
selector: "article"
---

# Overview - kitty

# Overview[¶](#overview "Link to this heading")

## Design philosophy[¶](#design-philosophy "Link to this heading")

*kitty* is designed for power keyboard users. To that end all its controls work
with the keyboard (although it fully supports mouse interactions as well). Its
configuration is a simple, human editable, single file for easy reproducibility
(I like to store configuration in source control).

The code in *kitty* is designed to be simple, modular and hackable. It is
written in a mix of C (for performance sensitive parts), Python (for easy
extensibility and flexibility of the UI) and Go (for the command line
[kittens](../glossary/#term-kittens)). It does not depend on any large and complex UI toolkit,
using only OpenGL for rendering everything.

Finally, *kitty* is designed from the ground up to support all modern terminal
features, such as Unicode, true color, bold/italic fonts, text formatting, etc.
It even extends existing text formatting escape codes, to add support for
features not available elsewhere, such as colored and styled (curly) underlines.
One of the design goals of *kitty* is to be easily extensible so that new
features can be added in the future with relatively little effort.

## Tabs and Windows[¶](#tabs-and-windows "Link to this heading")

*kitty* is capable of running multiple programs organized into tabs and windows.
The top level of organization is the [OS window](../glossary/#term-os_window). Each OS
window consists of one or more [tabs](../glossary/#term-tab). Each tab consists of one or more
[kitty windows](../glossary/#term-window). The kitty windows can be arranged in multiple
different [layouts](../glossary/#term-layout), like windows are organized in a tiling
window manager. The keyboard controls (which are [all customizable](../conf/#conf-kitty-shortcuts)) for tabs and windows are:

### Scrolling[¶](#scrolling "Link to this heading")

| Action | Shortcut |
| --- | --- |
| Line up | [`ctrl+shift+up`](../conf/#shortcut-kitty.Scroll-line-up) (also `⌥`+`⌘`+`⇞` and `⌘`+`↑` on macOS) |
| Line down | [`ctrl+shift+down`](../conf/#shortcut-kitty.Scroll-line-down) (also `⌥`+`⌘`+`⇟` and `⌘`+`↓` on macOS) |
| Page up | [`ctrl+shift+page_up`](../conf/#shortcut-kitty.Scroll-page-up) (also `⌘`+`⇞` on macOS) |
| Page down | [`ctrl+shift+page_down`](../conf/#shortcut-kitty.Scroll-page-down) (also `⌘`+`⇟` on macOS) |
| Top | [`ctrl+shift+home`](../conf/#shortcut-kitty.Scroll-to-top) (also `⌘`+`↖` on macOS) |
| Bottom | [`ctrl+shift+end`](../conf/#shortcut-kitty.Scroll-to-bottom) (also `⌘`+`↘` on macOS) |
| Previous shell prompt | [`ctrl+shift+z`](../conf/#shortcut-kitty.Scroll-to-previous-shell-prompt) (see [Shell integration](../shell-integration/#shell-integration)) |
| Next shell prompt | [`ctrl+shift+x`](../conf/#shortcut-kitty.Scroll-to-next-shell-prompt) (see [Shell integration](../shell-integration/#shell-integration)) |
| Browse scrollback in less | [`ctrl+shift+h`](../conf/#shortcut-kitty.Browse-scrollback-buffer-in-pager) |
| Browse last cmd output | [`ctrl+shift+g`](../conf/#shortcut-kitty.Browse-output-of-the-last-shell-command-in-pager) (see [Shell integration](../shell-integration/#shell-integration)) |

The scroll actions only take effect when the terminal is in the main screen.
When the alternate screen is active (for example when using a full screen
program like an editor) the key events are instead passed to program running in the
terminal.

### Tabs[¶](#tabs "Link to this heading")

| Action | Shortcut |
| --- | --- |
| New tab | [`ctrl+shift+t`](../conf/#shortcut-kitty.New-tab) (also `⌘`+`t` on macOS) |
| Close tab | [`ctrl+shift+q`](../conf/#shortcut-kitty.Close-tab) (also `⌘`+`w` on macOS) |
| Next tab | [`ctrl+shift+right`](../conf/#shortcut-kitty.Next-tab) (also `⇧`+`⌃`+`⇥` and `⇧`+`⌘`+`]` on macOS) |
| Previous tab | [`ctrl+shift+left`](../conf/#shortcut-kitty.Previous-tab) (also `⇧`+`⌃`+`⇥` and `⇧`+`⌘`+`[` on macOS) |
| Next layout | [`ctrl+shift+l`](../conf/#shortcut-kitty.Next-layout) |
| Move tab forward | [`ctrl+shift+.`](../conf/#shortcut-kitty.Move-tab-forward) |
| Move tab backward | [`ctrl+shift+,`](../conf/#shortcut-kitty.Move-tab-backward) |
| Set tab title | [`ctrl+shift+alt+t`](../conf/#shortcut-kitty.Set-tab-title) (also `⇧`+`⌘`+`i` on macOS) |

### Windows[¶](#windows "Link to this heading")

| Action | Shortcut |
| --- | --- |
| New window | [`ctrl+shift+enter`](../conf/#shortcut-kitty.New-window) (also `⌘`+`↩` on macOS) |
| New OS window | [`ctrl+shift+n`](../conf/#shortcut-kitty.New-OS-window) (also `⌘`+`n` on macOS) |
| Close window | [`ctrl+shift+w`](../conf/#shortcut-kitty.Close-window) (also `⇧`+`⌘`+`d` on macOS) |
| Resize window | [`ctrl+shift+r`](../conf/#shortcut-kitty.Start-resizing-window) (also `⌘`+`r` on macOS) |
| Next window | [`ctrl+shift+]`](../conf/#shortcut-kitty.Next-window) |
| Previous window | [`ctrl+shift+[`](../conf/#shortcut-kitty.Previous-window) |
| Move window forward | [`ctrl+shift+f`](../conf/#shortcut-kitty.Move-window-forward) |
| Move window backward | [`ctrl+shift+b`](../conf/#shortcut-kitty.Move-window-backward) |
| Move window to top | [`` ctrl+shift+` ``](../conf/#shortcut-kitty.Move-window-to-top) |
| Visually focus window | [`ctrl+shift+f7`](../conf/#shortcut-kitty.Visually-select-and-focus-window) |
| Visually swap window | [`ctrl+shift+f8`](../conf/#shortcut-kitty.Visually-swap-window-with-another) |
| Focus specific window | [`ctrl+shift+1`](../conf/#shortcut-kitty.First-window), [`ctrl+shift+2`](../conf/#shortcut-kitty.Second-window) … [`ctrl+shift+0`](../conf/#shortcut-kitty.Tenth-window) (also `⌘`+`1`, `⌘`+`2` … `⌘`+`9` on macOS) (clockwise from the top-left) |

Additionally, you can define shortcuts in `kitty.conf` to focus
neighboring windows and move windows around (similar to window movement in
**vim**):

```
map ctrl+left neighboring_window left
map shift+left move_window right
map ctrl+down neighboring_window down
map shift+down move_window up
...
```

You can also define a shortcut to switch to the previously active window:

```
map ctrl+p nth_window -1
```

[`nth_window`](../actions/#action-nth_window) will focus the nth window for positive numbers (starting from
zero) and the previously active windows for negative numbers.

To switch to the nth OS window, you can define [`nth_os_window`](../actions/#action-nth_os_window). Only
positive numbers are accepted, starting from one.

You can define shortcuts to detach the current window and move it to another tab
or another OS window:

```
# moves the window into a new OS window
map ctrl+f2 detach_window
# moves the window into a new tab
map ctrl+f3 detach_window new-tab
# moves the window into the previously active tab
map ctrl+f3 detach_window tab-prev
# moves the window into the tab at the left of the active tab
map ctrl+f3 detach_window tab-left
# moves the window into a new tab created to the left of the active tab
map ctrl+f3 detach_window new-tab-left
# asks which tab to move the window into
map ctrl+f4 detach_window ask
```

Similarly, you can detach the current tab, with:

```
# moves the tab into a new OS window
map ctrl+f2 detach_tab
# asks which OS Window to move the tab into
map ctrl+f4 detach_tab ask
```

Finally, you can define a shortcut to close all windows in a tab other than the
currently active window:

```
map f9 close_other_windows_in_tab
```

## Other keyboard shortcuts[¶](#other-keyboard-shortcuts "Link to this heading")

The full list of actions that can be mapped to key presses is available
[here](../actions/). To learn how to do more sophisticated keyboard
mappings, such as modal mappings, per application mappings, etc. see
[Making your keyboard dance](../mapping/).

| Action | Shortcut |
| --- | --- |
| Show this help | [`ctrl+shift+f1`](../conf/#shortcut-kitty.Show-documentation) |
| Copy to clipboard | [`ctrl+shift+c`](../conf/#shortcut-kitty.Copy-to-clipboard) (also `⌘`+`c` on macOS) |
| Paste from clipboard | [`ctrl+shift+v`](../conf/#shortcut-kitty.Paste-from-clipboard) (also `⌘`+`v` on macOS) |
| Paste from selection | [`ctrl+shift+s`](../conf/#shortcut-kitty.Paste-from-selection) |
| Pass selection to program | [`ctrl+shift+o`](../conf/#shortcut-kitty.Pass-selection-to-program) |
| Increase font size | [`ctrl+shift+equal`](../conf/#shortcut-kitty.Increase-font-size) (also `⌘`+`+` on macOS) |
| Decrease font size | [`ctrl+shift+minus`](../conf/#shortcut-kitty.Decrease-font-size) (also `⌘`+`-` on macOS) |
| Restore font size | [`ctrl+shift+backspace`](../conf/#shortcut-kitty.Reset-font-size) (also `⌘`+`0` on macOS) |
| Toggle fullscreen | [`ctrl+shift+f11`](../conf/#shortcut-kitty.Toggle-fullscreen) (also `⌃`+`⌘`+`f` on macOS) |
| Toggle maximized | [`ctrl+shift+f10`](../conf/#shortcut-kitty.Toggle-maximized) |
| Input Unicode character | [`ctrl+shift+u`](../conf/#shortcut-kitty.Unicode-input) (also `⌃`+`⌘`+`space` on macOS) |
| Open URL in web browser | [`ctrl+shift+e`](../conf/#shortcut-kitty.Open-URL) |
| Reset the terminal | [`ctrl+shift+delete`](../conf/#shortcut-kitty.Reset-the-terminal) (also `⌥`+`⌘`+`r` on macOS) |
| Edit `kitty.conf` | [`ctrl+shift+f2`](../conf/#shortcut-kitty.Edit-config-file) (also `⌘`+`,` on macOS) |
| Reload `kitty.conf` | [`ctrl+shift+f5`](../conf/#shortcut-kitty.Reload-kitty.conf) (also `⌃`+`⌘`+`,` on macOS) |
| Debug `kitty.conf` | [`ctrl+shift+f6`](../conf/#shortcut-kitty.Debug-kitty-configuration) (also `⌥`+`⌘`+`,` on macOS) |
| Open a *kitty* shell | [`ctrl+shift+escape`](../conf/#shortcut-kitty.Open-the-kitty-command-shell) |
| Increase background opacity | [`ctrl+shift+a>m`](../conf/#shortcut-kitty.Increase-background-opacity) |
| Decrease background opacity | [`ctrl+shift+a>l`](../conf/#shortcut-kitty.Decrease-background-opacity) |
| Full background opacity | [`ctrl+shift+a>1`](../conf/#shortcut-kitty.Make-background-fully-opaque) |
| Reset background opacity | [`ctrl+shift+a>d`](../conf/#shortcut-kitty.Reset-background-opacity) |

## Configuring kitty[¶](#configuring-kitty "Link to this heading")

*kitty* is highly configurable, everything from keyboard shortcuts to painting
frames-per-second. Press [`ctrl+shift+f2`](../conf/#shortcut-kitty.Edit-config-file) in kitty to open its fully
commented sample config file in your text editor. For details see the
[configuration docs](../conf/).

## Layouts[¶](#layouts "Link to this heading")

A [layout](../glossary/#term-layout) is an arrangement of multiple [kitty windows](../glossary/#term-window)
inside a top-level [OS window](../glossary/#term-os_window). The layout manages all its
windows automatically, resizing and moving them as needed. You can create a new
[window](../glossary/#term-window) using the [`ctrl+shift+enter`](../conf/#shortcut-kitty.New-window) key combination.

Currently, there are seven layouts available:

* **Fat** -- One (or optionally more) windows are shown full width on the top,
  the rest of the windows are shown side-by-side on the bottom
* **Grid** -- All windows are shown in a grid
* **Horizontal** -- All windows are shown side-by-side
* **Splits** -- Windows arranged in arbitrary patterns created using horizontal
  and vertical splits
* **Stack** -- Only a single maximized window is shown at a time
* **Tall** -- One (or optionally more) windows are shown full height on the
  left, the rest of the windows are shown one below the other on the right
* **Vertical** -- All windows are shown one below the other

By default, all layouts are enabled and you can switch between layouts using
the [`ctrl+shift+l`](../conf/#shortcut-kitty.Next-layout) key combination. You can also create shortcuts to select
particular layouts, and choose which layouts you want to enable, see
[Layout management](../conf/#conf-kitty-shortcuts-layout) for examples. The first layout listed in
[`enabled_layouts`](../conf/#opt-kitty.enabled_layouts) becomes the default layout.

For more details on the layouts and how to use them see [the documentation](../layouts/).

## Extending kitty[¶](#extending-kitty "Link to this heading")

kitty has a powerful framework for scripting. You can create small terminal
programs called [kittens](../kittens_intro/). These can be used to add features
to kitty, for example, [editing remote files](../kittens/remote_file/) or
[inputting Unicode characters](../kittens/unicode_input/). They can also be
used to create programs that leverage kitty’s powerful features, for example,
[viewing images](../kittens/icat/) or [diffing files with image support](../kittens/diff/).

You can [create your own kittens to scratch your own itches](../kittens/custom/).

For a list of all the builtin kittens, [see here](../kittens_intro/#kittens).

Additionally, you can use the [watchers](../launch/#watchers) framework
to create Python scripts that run in response to various events such as windows
being resized, closing, having their titles changed, etc.

## Remote control[¶](#remote-control "Link to this heading")

*kitty* has a very powerful system that allows you to control it from the
[shell prompt, even over SSH](../remote-control/). You can change colors,
fonts, open new [windows](../glossary/#term-window), [tabs](../glossary/#term-tab), set their titles,
change window layout, get text from one window and send text to another, etc.
The possibilities are endless. See the [tutorial](../remote-control/) to get
started.

## Sessions[¶](#sessions "Link to this heading")

You can control the [tabs](../glossary/#term-tab), [kitty window](../glossary/#term-window) layout,
working directory, startup programs, etc. by creating a *session* file and using
the [`kitty --session`](../invocation/#cmdoption-kitty-session) command line flag or the [`startup_session`](../conf/#opt-kitty.startup_session)
option in `kitty.conf`. You can also easily switch between sessions with
a keypress. See [Sessions](../sessions/) for details.

## Creating tabs/windows[¶](#creating-tabs-windows "Link to this heading")

kitty can be told to run arbitrary programs in new [tabs](../glossary/#term-tab),
[windows](../glossary/#term-window) or [overlays](../glossary/#term-overlay) at a keypress.
To learn how to do this, see [here](../launch/).

## Mouse features[¶](#mouse-features "Link to this heading")

* You can click on a URL to open it in a browser.
* You can double click to select a word and then drag to select more words.
* You can triple click to select a line and then drag to select more lines.
* You can triple click while holding `Ctrl`+`Alt` to select from clicked
  point to end of line.
* You can right click to extend a previous selection.
* You can hold down `Ctrl`+`Alt` and drag with the mouse to select in
  columns.
* Selecting text automatically copies it to the primary clipboard (on platforms
  with a primary clipboard).
* You can middle click to paste from the primary clipboard (on platforms with a
  primary clipboard).
* You can right click while holding `Ctrl`+`Shift` to open the output of the
  clicked on command in a pager (requires [Shell integration](../shell-integration/#shell-integration))
* You can select text with kitty even when a terminal program has grabbed the
  mouse by holding down the `Shift` key

All these actions can be customized in `kitty.conf` as described
[here](../conf/#conf-kitty-mouse-mousemap).

You can also customize what happens when clicking on [hyperlinks](../glossary/#term-hyperlinks) in
kitty, having it open files in your editor, download remote files, open things
in your browser, etc. For details, see [here](../open_actions/).

## Font control[¶](#font-control "Link to this heading")

*kitty* has extremely flexible and powerful font selection features. You can
specify individual families for the regular, bold, italic and bold+italic fonts.
You can even specify specific font families for specific ranges of Unicode
characters. This allows precise control over text rendering. It can come in
handy for applications like powerline, without the need to use patched fonts.
See the various font related configuration directives in
[Fonts](../conf/#conf-kitty-fonts).

## The scrollback buffer[¶](#the-scrollback-buffer "Link to this heading")

*kitty* supports scrolling back to view history, just like most terminals. You
can use either keyboard shortcuts or the mouse scroll wheel to do so. *kitty*
displays an interactive [`scrollbar`](../conf/#opt-kitty.scrollbar) along the right edge
of the window that shows your current position in the scrollback. You can click
and drag the scrollbar to quickly navigate through the history.

However, *kitty* has an extra, neat feature. Sometimes you need to explore the scrollback
buffer in more detail, maybe search for some text or refer to it side-by-side
while typing in a follow-up command. *kitty* allows you to do this by pressing
the [`ctrl+shift+h`](../conf/#shortcut-kitty.Browse-scrollback-buffer-in-pager) shortcut, which will open the scrollback buffer in
your favorite pager program (which is **less** by default). Colors and
text formatting are preserved. You can explore the scrollback buffer comfortably
within the pager.

Additionally, you can pipe the contents of the scrollback buffer to an
arbitrary, command running in a new [window](../glossary/#term-window), [tab](../glossary/#term-tab) or
[overlay](../glossary/#term-overlay). For example:

```
map f1 launch --stdin-source=@screen_scrollback --stdin-add-formatting less +G -R
```

Would open the scrollback buffer in a new [window](../glossary/#term-window) when you press the
`F1` key. See [`show_scrollback`](../conf/#shortcut-kitty.Browse-scrollback-buffer-in-pager) for details.

If you want to use it with an editor such as **nvim** to get more powerful
features, see for example, [kitty-scrollback.nvim](https://github.com/mikesmithgh/kitty-scrollback.nvim) or [kitty-grab](https://github.com/yurikhan/kitty_grab)
or see more tips for using various editor programs, in [this thread](https://github.com/kovidgoyal/kitty/issues/719).

If you wish to store very large amounts of scrollback to view using the piping
or [`show_scrollback`](../conf/#shortcut-kitty.Browse-scrollback-buffer-in-pager) features, you can use the
[`scrollback_pager_history_size`](../conf/#opt-kitty.scrollback_pager_history_size) option.

## Integration with shells[¶](#integration-with-shells "Link to this heading")

kitty has the ability to integrate closely within common shells, such as [zsh](https://www.zsh.org/), [fish](https://fishshell.com) and [bash](https://www.gnu.org/software/bash/) to enable features such as jumping to
previous prompts in the scrollback, viewing the output of the last command in
**less**, using the mouse to move the cursor while editing prompts, etc.
See [Shell integration](../shell-integration/) for details.

## Multiple copy/paste buffers[¶](#multiple-copy-paste-buffers "Link to this heading")

In addition to being able to copy/paste from the system clipboard, in *kitty*
you can also setup an arbitrary number of copy paste buffers. To do so, simply
add something like the following to your `kitty.conf`:

```
map f1 copy_to_buffer a
map f2 paste_from_buffer a
```

This will allow you to press `F1` to copy the current selection to an
internal buffer named `a` and `F2` to paste from that buffer. The buffer
names are arbitrary strings, so you can define as many such buffers as you need.

## Marks[¶](#marks "Link to this heading")

kitty has the ability to mark text on the screen based on regular expressions.
This can be useful to highlight words or phrases when browsing output from long
running programs or similar. To learn how this feature works, see [Mark text on screen](../marks/).
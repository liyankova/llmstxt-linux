---
source_url: "https://yazi-rs.github.io/docs/configuration/keymap"
title: "keymap.toml | Yazi"
crawl_date: "2025-11-16T14:55:25.433903Z"
selector: "article"
---

# keymap.toml | Yazi

* [Configuration](/docs/configuration/overview)
* keymap.toml
Version: 25.5.31

On this page

info

If you want to fine-tune the default settings, the first step is to [create your own configuration file](/docs/configuration/overview).

You can change Yazi's keybindings in your `keymap.toml` file, which consists of the following 8 layers:

* [[mgr]](#mgr) - File list.
* [[tasks]](#tasks) - Task manager.
* [[spot]](#spot) - File information spotter.
* [[pick]](#pick) - Pick component. e.g. "open with" for files.
* [[input]](#input) - Input component. e.g. create, rename, etc.
* [[confirm]](#confirm) - Confirmation dialog. e.g. remove, overwrite, etc.
* [[cmp]](#cmp) - Completion component. e.g. "cd" path completion.
* [[help]](#help) - Help menu.

In each layer, there are two attributes: `prepend_keymap` and `append_keymap`.
Prepend inserts before [the default keybindings](https://github.com/sxyazi/yazi/blob/shipped/yazi-config/preset/keymap-default.toml), while append inserts after them.

Since Yazi selects the first matching key to run, prepend always has a higher priority than default, and append always has a lower priority than default:

```
[mgr]  
prepend_keymap = [  
	{ on = "<C-a>", run = "my-cmd1", desc = "Single command with `Ctrl + a`" },  
]  
append_keymap = [  
	{ on = [ "g", "b" ], run = "my-cmd2",          desc = "Single command with `g => b`" },  
	{ on = "c",          run = [ "cmd1", "cmd2" ], desc = "Multiple commands with `c`" }  
]
```

Or in another different style:

```
[[mgr.prepend_keymap]]  
on   = "<C-a>"  
run  = "my-cmd1"  
desc = "Single command with `Ctrl + a`"  
  
[[mgr.append_keymap]]  
on  = [ "g", "b" ]  
run = "my-cmd2"  
desc = "Single command with `g => b`"  
  
[[mgr.append_keymap]]  
on  = "c"  
run = [ "my-cmd1", "my-cmd2" ]  
desc = "Multiple commands with `c`"
```

But keep in mind that you can only choose one of them, and it cannot be a combination of the two, as TOML language does not allow this:

```
[mgr]  
prepend_keymap = [  
	{ on = "<C-a>", run = "my-cmd1" },  
]  
  
[[mgr.append_keymap]]  
on  = [ "g", "b" ]  
run = "my-cmd2"
```

When you don't need any default and want to fully customize your keybindings, use `keymap`, for example:

```
[mgr]  
keymap = [  
	# This will override all default keybindings, and just keep the two below.  
	{ on = "<C-a>",      run = "my-cmd1" },  
	{ on = [ "g", "b" ], run = "my-cmd2" },  
]
```

## Key notation[​](#notation "Direct link to Key notation")

You can specify one or more keys in the `on` of each keybinding rule, and each key can be represented with the following notations:

| Notation | Description | Notation | Description |
| --- | --- | --- | --- |
| `a` - `z` | Lowercase letters | `A` - `Z` | Uppercase letters |
| `<Space>` | Space key | `<Backspace>` | Backspace key |
| `<Enter>` | Enter key | - | - |
| `<Left>` | Left arrow key | `<Right>` | Right arrow key |
| `<Up>` | Up arrow key | `<Down>` | Down arrow key |
| `<Home>` | Home key | `<End>` | End key |
| `<PageUp>` | PageUp key | `<PageDown>` | PageDown key |
| `<Tab>` | Tab key | `<BackTab>` | Shift + Tab key |
| `<Delete>` | Delete key | `<Insert>` | Insert key |
| `<F1>` - `<F19>` | Function keys | `<Esc>` | Escape key |

You can combine the following modifiers for the keys above:

| Modifier | Description |
| --- | --- |
| `<S-…>` | Shift key. |
| `<C-…>` | Ctrl key. |
| `<A-…>` | Alt/Meta key. |
| `<D-…>` | Command/Windows/Super key. |

For example:

* `<C-a>` for `Ctrl` + `a`.
* `<C-S-b>` or `<C-B>` for `Ctrl` + `Shift` + `b`.

Note that:

1. Not all terminals support `<D-...>` - make sure your terminal supports and has [CSI u](https://sw.kovidgoyal.net/kitty/keyboard-protocol/) enabled if you want to use it.
2. macOS doesn't have an `Alt` key, so `<A-...>` won't work. Some terminals offer a setting to map the `Option` as the `Alt` key, make sure you have it enabled.
3. The [legacy terminal keyboard protocol](https://en.wikipedia.org/wiki/Control_character) treats `<Tab>` and `<C-i>`, `<Enter>` and `<C-m>`, etc. as the same key. If you want to distinguish between them, make sure your terminal supports and has [CSI u](https://sw.kovidgoyal.net/kitty/keyboard-protocol/) enabled.

## [mgr][​](#mgr "Direct link to [mgr]")

### `escape`[​](#mgr.escape "Direct link to mgr.escape")

Cancel find, exit visual mode, clear selected, cancel filter, or cancel search.

| Argument/Option | Description |
| --- | --- |
| `--all` | Do all the below. |
| `--find` | Cancel find. |
| `--visual` | Exit visual mode. |
| `--select` | Clear selected. |
| `--filter` | Cancel filter. |
| `--search` | Cancel search. |

Automatically determine the operation by default, and it will only execute the selected operation after specifying the option; multiple options can be stacked.

### `quit`[​](#mgr.quit "Direct link to mgr.quit")

Exit the process.

| Argument/Option | Description |
| --- | --- |
| `--no-cwd-file` | Don't output the current directory to the file specified by `yazi --cwd-file`. |

### `close`[​](#mgr.close "Direct link to mgr.close")

Close the current tab; if it's the last tab, exit the process instead.

| Argument/Option | Description |
| --- | --- |
| `--no-cwd-file` | Don't output the current directory to the file specified by `yazi --cwd-file` on exit. |

### `suspend`[​](#mgr.suspend "Direct link to mgr.suspend")

Pauses Yazi and returns to the parent shell to continue with other tasks.

Once those tasks are done, use the `fg` command of the shell to send a resume signal and return back to Yazi.

### `arrow`[​](#mgr.arrow "Direct link to mgr.arrow")

| Argument/Option | Description |
| --- | --- |
| `[steps]` | The number of steps the cursor moves up or down. |

`[steps]` can be one of the following values:

| Value | Description |
| --- | --- |
| `n` | Move the cursor `n` lines up or down, negative for up, positive for down. |
| `n%` | Move the cursor `n%` of the screen height up or down, negative for up, positive for down. |
| `"top"` | Move the cursor to the top (first item). |
| `"bot"` | Move the cursor to the bottom (last item). |
| `"prev"` | Go to the previous item, or the bottom if the cursor is at the top. |
| `"next"` | Go to the next item, or the top if the cursor is at the bottom. |

The `arrow prev`/`arrow next` commands are similar to `arrow -1`/`arrow 1`, except that the former supports wraparound scrolling.

### `leave`[​](#mgr.leave "Direct link to mgr.leave")

Go back to the parent directory of the hovered file, or the parent of the current working directory if no file is hovered on.

### `enter`[​](#mgr.enter "Direct link to mgr.enter")

Enter the child directory.

### `back`[​](#mgr.back "Direct link to mgr.back")

Go back to the previous directory.

### `forward`[​](#mgr.forward "Direct link to mgr.forward")

Go forward to the next directory.

### `seek`[​](#mgr.seek "Direct link to mgr.seek")

Scroll the contents in the preview panel.

| Argument/Option | Description |
| --- | --- |
| `[n]` | Use negative values to seek up and positive values to seek down. |

### `spot`[​](#mgr.spot "Direct link to mgr.spot")

Display file information with the preset or user-customized spotter.

### `cd`[​](#mgr.cd "Direct link to mgr.cd")

Change the current directory.

| Argument/Option | Description |
| --- | --- |
| `[path]` | The path to change to. |
| `--interactive` | Use an interactive UI to input the path. |

You can add your own `g` series keys to achieve a simple bookmark feature:

```
[[mgr.prepend_keymap]]  
on   = [ "g", "d" ]  
run  = "cd ~/Downloads"  
desc = "Cd to ~/Downloads"  
  
[[mgr.prepend_keymap]]  
on   = [ "g", "p" ]  
run  = "cd ~/Pictures"  
desc = "Cd to ~/Pictures"
```

For Windows users, you can also switch drives using the `cd` command:

```
[[mgr.prepend_keymap]]  
on   = [ "g", "d" ]  
run  = "cd D:"  
desc = "Switch to D drive"  
  
[[mgr.prepend_keymap]]  
on   = [ "g", "p" ]  
run  = 'cd "E:\\Pictures"'  # We need to escape the backslash  
desc = 'Cd to E:\Pictures'
```

Check out the [resources page](/docs/resources) for a more comprehensive bookmark plugin.

### `reveal`[​](#mgr.reveal "Direct link to mgr.reveal")

Hover on the specified file.

If the file is not in the current directory, it will change the current directory to the file's parent.

| Argument/Option | Description |
| --- | --- |
| `[path]` | The path to reveal. |

### `toggle`[​](#mgr.toggle "Direct link to mgr.toggle")

Toggle the selection state of the hovered file.

| Argument/Option | Description |
| --- | --- |
| N/A | Reverse the selection. |
| `--state=on` | Select the file. |
| `--state=off` | Deselect the file. |

### `toggle_all`[​](#mgr.toggle_all "Direct link to mgr.toggle_all")

Toggle the selection state of all files in the current working directory.

| Argument/Option | Description |
| --- | --- |
| N/A | Reverse the selections. |
| `--state=on` | Select the files. |
| `--state=off` | Deselect the files. |

Note that `toggle_all --state=off` only deselect the files in CWD, if you have selected files across multiple directories, and want to deselect all of them, use [`escape --select`](#mgr.escape).

### `visual_mode`[​](#mgr.visual_mode "Direct link to mgr.visual_mode")

Enter visual mode.

| Argument/Option | Description |
| --- | --- |
| N/A | Selection mode. |
| `--unset` | Unset mode. |

### `open`[​](#mgr.open "Direct link to mgr.open")

Open the selected files using [the rules in `[open]`](/docs/configuration/yazi#open).

| Argument/Option | Description |
| --- | --- |
| `--interactive` | Open the hovered/selected file(s) with an interactive UI to choose the opening method. |
| `--hovered` | Always open the hovered file regardless of the selection state. |

### `yank`[​](#mgr.yank "Direct link to mgr.yank")

Yank the selected files.

| Argument/Option | Description |
| --- | --- |
| N/A | Copy mode. |
| `--cut` | Cut mode. |

### `unyank`[​](#mgr.unyank "Direct link to mgr.unyank")

Cancel the yank status of files.

### `paste`[​](#mgr.paste "Direct link to mgr.paste")

Paste the yanked files.

| Argument/Option | Description |
| --- | --- |
| `--force` | Overwrite the destination file if it exists. |
| `--follow` | Copy the file pointed to by a symbolic link, rather than the link itself. Only can be used during copying. |

### `link`[​](#mgr.link "Direct link to mgr.link")

Create a symbolic link to the yanked files. (This is a privileged action on Windows and must be run as an administrator.)

| Argument/Option | Description |
| --- | --- |
| `--relative` | Use a relative path for the symbolic link. |
| `--force` | Overwrite the destination file if it exists. |

### `hardlink`[​](#mgr.hardlink "Direct link to mgr.hardlink")

Hardlink the yanked files.

| Argument/Option | Description |
| --- | --- |
| `--force` | Overwrite the destination file if it exists. |
| `--follow` | Hardlink the file pointed to by a symbolic link, not the symlink itself. |

### `remove`[​](#mgr.remove "Direct link to mgr.remove")

Move the files to the trash/recycle bin on macOS/Windows. For Linux, it will follow [The FreeDesktop.org Trash specification](https://specifications.freedesktop.org/trash-spec/1.0/).

In the Android platform, you can only use it with the `--permanently` option, since there lacks the concept of a trash bin.

| Argument/Option | Description |
| --- | --- |
| `--force` | Don't show the confirmation dialog, and trash/delete files directly. |
| `--permanently` | Permanently delete the files. |
| `--hovered` | Always remove the hovered file regardless of the selection state. |

### `create`[​](#mgr.create "Direct link to mgr.create")

Create a file or directory. Ends with `/` (Unix) or `\` (Windows) for directories.

| Argument/Option | Description |
| --- | --- |
| `--dir` | Always create directories, regardless of whether end with `/` or `\`. |
| `--force` | Overwrite the destination file directly if it exists, without showing the confirmation dialog. |

### `rename`[​](#mgr.rename "Direct link to mgr.rename")

Rename a file or directory, or bulk rename if multiple files are selected (`$EDITOR` is used to edit the filenames by default, see [Specify a different editor for bulk renaming](/docs/tips#bulk-editor) for details).

* `--hovered`: Always rename the hovered file regardless of the selection state.
* `--force`: Overwrite the destination file directly if it exists, without showing the confirmation dialog.
* `--empty`: Empty a part of the filename.
  + `"stem"`: Empty the stem. e.g. `"foo.jpg"` -> `".jpg"`.
  + `"ext"`: Empty the extension. e.g. `"foo.jpg"` -> `"foo."`.
  + `"dot_ext"`: Empty the dot and extension. e.g. `"foo.jpg"` -> `"foo"`.
  + `"all"`: Empty the whole filename. e.g. `"foo.jpg"` -> `""`.
* `--cursor`: Specify the cursor position of the renaming input box.
  + `"end"`: The end of the filename.
  + `"start"`: The start of the filename.
  + `"before_ext"`: Before the extension of the filename.

You can also use `--cursor` with `--empty`, for example, `rename --empty=stem --cursor=start` will empty the file's stem, and move the cursor to the start.

Which causes the input box content for the filename `foo.jpg` to be `|.jpg`, where "|" represents the cursor position.

### `copy`[​](#mgr.copy "Direct link to mgr.copy")

Copy the path of files or directories that are selected or hovered on.

| Argument/Option | Description |
| --- | --- |
| `[what]` | What to copy, see the table below. |
| `--separator` | Path separator, see the table below. |
| `--hovered` | Always copy the hovered file regardless of the selection state. |

`[what]` can be one of the following values:

| Value | Description |
| --- | --- |
| `"path"` | Absolute path. |
| `"dirname"` | Path of the parent directory. |
| `"filename"` | Name of the file. |
| `"name_without_ext"` | Name of the file without the extension. |

`--separator` can be one of the following values:

| Value | Description |
| --- | --- |
| N/A | Platform-specific separator, e.g. `\` for Windows and `/` for Unix. |
| `"unix"` | Use `/` for all platforms. |

### `shell`[​](#mgr.shell "Direct link to mgr.shell")

Run a shell command.

| Argument/Option | Description |
| --- | --- |
| `[template]` | Optional, command template to be run. |
| `--block` | Open in a blocking manner. After setting this, Yazi will hide into a secondary screen and display the program on the main screen until it exits. During this time, it can receive I/O signals, which is useful for interactive programs. |
| `--orphan` | Keep the process running even if Yazi has exited, once specified, the process will be detached from the task scheduling system. |
| `--interactive` | Request the user to input the command to be run interactively |
| `--cursor` | Set the initial position of the cursor in the interactive command input box. For example, `shell 'zip -r .zip "$0"' --cursor=7 --interactive` places the cursor before `.zip`. |

You can use the following shell variables in `[template]`:

* `$n` (Unix) / `%n` (Windows): The N-th selected file, starting from `1`. e.g. `$2` represents the second selected file.
* `$@` (Unix) / `%*` (Windows): All selected files, i.e. `$1`, `$2`, ..., `$n`.
* `$0` (Unix) / `%0` (Windows): The hovered file.
* Note that, these variables follow platform-specific differences. For example, Unix shell requires wrapping `$` with quotes, while `%` in Windows batch scripts doesn't. Refer to the documentation of `sh` and `cmd.exe` for details.

You can use an end-of-options marker (`--`) to avoid any escaping - everything following the `--` will be treated as a raw string:

```
[[mgr.prepend_keymap]]  
on = "d"  
- run = "shell 'trash-put \"$@\"'"  
+ run = 'shell -- trash-put "$@"'  
desc = "Trash selected files"
```

For complex shell scripts, you can use TOML's basic strings (`'''` or `"""`) to write them in multiple lines, as demonstrated in [this tip](/docs/tips#email-selected-files).

### `hidden`[​](#mgr.hidden "Direct link to mgr.hidden")

Set the visibility of hidden files.

| Argument/Option | Description |
| --- | --- |
| `"show"` | Show hidden files. |
| `"hide"` | Hide hidden files. |
| `"toggle"` | Toggle the hidden state. |

### `linemode`[​](#mgr.linemode "Direct link to mgr.linemode")

Set the [line mode](/docs/configuration/yazi#mgr.linemode).

| Argument/Option | Description |
| --- | --- |
| `"none"` | No line mode. |
| `"size"` | Display the size in bytes of the file. Note that currently directory sizes are only evaluated when [`sort_by = "size"`](/docs/configuration/yazi#mgr.sort_by), and this might change in the future. |
| `"btime"` | Display the birth time of the file. |
| `"mtime"` | Display the last modified time of the file. |
| `"permissions"` | Display the permissions of the file, only available on Unix-like systems. |
| `"owner"` | Display the owner of the file, only available on Unix-like systems. |

### `search`[​](#mgr.search "Direct link to mgr.search")

| Argument/Option | Description |
| --- | --- |
| `--via` | Search engine, available values: [`fd`](https://github.com/sharkdp/fd), [`rg`](https://github.com/BurntSushi/ripgrep), and [`rga`](https://github.com/phiresky/ripgrep-all) |
| `--args` | Additional arguments passed to the specified engine, for example `search --via=fd --args='-e -H'` |

You can search with an empty keyword (`""`) via `fd` to achieve flat view.

Demonstrate flat view

Original post: <https://github.com/sxyazi/yazi/issues/676#issuecomment-1943494129>

[](https://github.com/sxyazi/yazi/assets/17523360/d2c9df9b-b7ef-41ec-889f-26b2f1117cd0)

Or bind a key to the `search_do` command to quickly switch to the flat view:

```
[[mgr.prepend_keymap]]  
on   = [ "g", "f" ]  
run  = 'search_do --via=fd --args="-d 3"'  
desc = "Switch to the flat view with a max depth of 3"
```

### `find`[​](#mgr.find "Direct link to mgr.find")

Find files in the current working directory interactively and incrementally.

| Argument/Option | Description |
| --- | --- |
| `--previous` | Find for the previous occurrence. |
| `--smart` | Use smart-case when finding, i.e. case-sensitive if the query contains uppercase characters, otherwise case-insensitive. |
| `--insensitive` | Use case-insensitive find. |

### `find_arrow`[​](#mgr.find_arrow "Direct link to mgr.find_arrow")

Move the cursor to the next or previous occurrence.

| Argument/Option | Description |
| --- | --- |
| `--previous` | Move to the previous occurrence. |

### `filter`[​](#mgr.filter "Direct link to mgr.filter")

| Argument/Option | Description |
| --- | --- |
| `--smart` | Filter with smart-case, i.e. case-sensitive if the keyword contains uppercase characters, otherwise case-insensitive. |
| `--insensitive` | Use case-insensitive filter. |

### `sort`[​](#mgr.sort "Direct link to mgr.sort")

* `[by]`: Optional, if not provided, the sort method will be kept unchanged.
  + `"none"`: Don't sort.
  + `"mtime"`: Sort by last modified time.
  + `"btime"`: Sort by birth time.
  + `"extension"`: Sort by file extension.
  + `"alphabetical"`: Sort alphabetically, e.g. `1.md` < `10.md` < `2.md`
  + `"natural"`: Sort naturally, e.g. `1.md` < `2.md` < `10.md`
  + `"size"`: Sort by file size.
  + `"random"`: Sort randomly.
* `--reverse`: Display files in reverse order. `--reverse` or `--reverse=yes` to enable, `--reverse=no` to disable.
* `--dir-first`: Display directories first. `--dir-first` or `--dir-first=yes` to enable, `--dir-first=no` to disable.
* `--translit`: Transliterate filenames for sorting, see [sort\_translit](/docs/configuration/yazi#mgr.sort_translit) for details. `--translit` or `--translit=yes` to enable, `--translit=no` to disable.

### `tab_create`[​](#mgr.tab_create "Direct link to mgr.tab_create")

| Argument/Option | Description |
| --- | --- |
| `[path]` | Optional, create a new tab using the specified path. |
| `--current` | Optional, create a new tab using the current path. |

If neither `[path]` nor `--current` is specified, will use the startup directory to create the tab.

### `tab_close`[​](#mgr.tab_close "Direct link to mgr.tab_close")

| Argument/Option | Description |
| --- | --- |
| `[n]` | Close the tab at position `n`, starting from 0. |

If you want to close the current tab, use the [`close`](/docs/configuration/keymap/#mgr.close) command instead.

### `tab_switch`[​](#mgr.tab_switch "Direct link to mgr.tab_switch")

| Argument/Option | Description |
| --- | --- |
| `[n]` | Switch to the tab at position `n`, starting from 0. |
| `--relative` | Switch to the tab at a position relative to the current tab. The value of `n` can be negative when using this parameter. |

### `tab_swap`[​](#mgr.tab_swap "Direct link to mgr.tab_swap")

| Argument/Option | Description |
| --- | --- |
| `[n]` | Swap the current tab with the tab at position `n`, where negative values move the tab forward, and positive values move it backward. |

### `help`[​](#mgr.help "Direct link to mgr.help")

Open the help menu.

### `plugin`[​](#mgr.plugin "Direct link to mgr.plugin")

See [Functional plugin](/docs/plugins/overview#functional-plugin).

### `noop`[​](#mgr.noop "Direct link to mgr.noop")

If you want to disable certain preset keybindings without rewriting the entire `keymap`, you can use the virtual `noop` command.

For example, to disable the default keybinding of `g` ⇒ `c`, use:

```
[[mgr.prepend_keymap]]  
on  = [ "g", "c" ]  
run = "noop"
```

Or, if you prefer an array style:

```
[[mgr.prepend_keymap]]  
on  = [ "g", "c" ]  
run = [ "noop" ]  # The array can only have one element and must be "noop"
```

The disabled keys won't trigger any actions when pressed and won't show up in the `which` component.

## [tasks][​](#tasks "Direct link to [tasks]")

### `show`[​](#tasks.show "Direct link to tasks.show")

Show the task manager.

### `close`[​](#tasks.close "Direct link to tasks.close")

Hide the task manager.

### `arrow`[​](#tasks.arrow "Direct link to tasks.arrow")

| Argument/Option | Description |
| --- | --- |
| `[steps]` | The number of steps the cursor moves up or down. |

`[steps]` can be one of the following values:

| Value | Description |
| --- | --- |
| `n` | Move the cursor `n` lines up or down, negative for up, positive for down. |
| `n%` | Move the cursor `n%` of the screen height up or down, negative for up, positive for down. |
| `"top"` | Move the cursor to the top (first item). |
| `"bot"` | Move the cursor to the bottom (last item). |
| `"prev"` | Go to the previous item, or the bottom if the cursor is at the top. |
| `"next"` | Go to the next item, or the top if the cursor is at the bottom. |

The `arrow prev`/`arrow next` commands are similar to `arrow -1`/`arrow 1`, except that the former supports wraparound scrolling.

### `inspect`[​](#tasks.inspect "Direct link to tasks.inspect")

Inspect the task log:

* I/O error for failed file operations
* Lua error for failed async plugin tasks
* Real-time stdout/stderr for background running or failed shell tasks

press `q` to exit the inspect view.

### `cancel`[​](#tasks.cancel "Direct link to tasks.cancel")

Cancel the task.

### `help`[​](#tasks.help "Direct link to tasks.help")

Open the help menu.

### `plugin`[​](#tasks.plugin "Direct link to tasks.plugin")

See [Functional plugin](/docs/plugins/overview#functional-plugin).

### `noop`[​](#tasks.noop "Direct link to tasks.noop")

See [`noop` command](#mgr.noop).

## [spot][​](#spot "Direct link to [spot]")

### `close`[​](#spot.close "Direct link to spot.close")

Hide the spotter.

### `arrow`[​](#spot.arrow "Direct link to spot.arrow")

| Argument/Option | Description |
| --- | --- |
| `[steps]` | The number of steps the cursor moves up or down. |

`[steps]` can be one of the following values:

| Value | Description |
| --- | --- |
| `n` | Move the cursor `n` lines up or down, negative for up, positive for down. |
| `n%` | Move the cursor `n%` of the screen height up or down, negative for up, positive for down. |
| `"top"` | Move the cursor to the top (first item). |
| `"bot"` | Move the cursor to the bottom (last item). |
| `"prev"` | Go to the previous item, or the bottom if the cursor is at the top. |
| `"next"` | Go to the next item, or the top if the cursor is at the bottom. |

The `arrow prev`/`arrow next` commands are similar to `arrow -1`/`arrow 1`, except that the former supports wraparound scrolling.

### `swipe`[​](#spot.swipe "Direct link to spot.swipe")

| Argument/Option | Description |
| --- | --- |
| `[n]` | Swipe `n` files up or down in the file list. Negative value for up, positive value for down. |

### `copy`[​](#spot.copy "Direct link to spot.copy")

Copy the content from the spotter.

| Argument/Option | Description |
| --- | --- |
| `"cell"` | Copy the selected table cell |

### `plugin`[​](#spot.plugin "Direct link to spot.plugin")

See [Functional plugin](/docs/plugins/overview#functional-plugin).

### `noop`[​](#spot.noop "Direct link to spot.noop")

See [`noop` command](#mgr.noop).

### `help`[​](#spot.help "Direct link to spot.help")

Open the help menu.

## [pick][​](#pick "Direct link to [pick]")

### `close`[​](#pick.close "Direct link to pick.close")

Cancel the picker.

| Argument/Option | Description |
| --- | --- |
| `--submit` | Submit the picker. |

### `arrow`[​](#pick.arrow "Direct link to pick.arrow")

| Argument/Option | Description |
| --- | --- |
| `[steps]` | The number of steps the cursor moves up or down. |

`[steps]` can be one of the following values:

| Value | Description |
| --- | --- |
| `n` | Move the cursor `n` lines up or down, negative for up, positive for down. |
| `n%` | Move the cursor `n%` of the screen height up or down, negative for up, positive for down. |
| `"top"` | Move the cursor to the top (first item). |
| `"bot"` | Move the cursor to the bottom (last item). |
| `"prev"` | Go to the previous item, or the bottom if the cursor is at the top. |
| `"next"` | Go to the next item, or the top if the cursor is at the bottom. |

The `arrow prev`/`arrow next` commands are similar to `arrow -1`/`arrow 1`, except that the former supports wraparound scrolling.

### `help`[​](#pick.help "Direct link to pick.help")

Open the help menu.

### `plugin`[​](#pick.plugin "Direct link to pick.plugin")

See [Functional plugin](/docs/plugins/overview#functional-plugin).

### `noop`[​](#pick.noop "Direct link to pick.noop")

See [`noop` command](#mgr.noop).

## [input][​](#input "Direct link to [input]")

### `close`[​](#input.close "Direct link to input.close")

Cancel input.

| Argument/Option | Description |
| --- | --- |
| `--submit` | Submit the input. |

### `escape`[​](#input.escape "Direct link to input.escape")

Go back the normal mode, or cancel input.

### `move`[​](#input.move "Direct link to input.move")

Move the cursor left or right.

| Argument/Option | Description |
| --- | --- |
| `[n]` | Move the cursor `n` characters left or right. Negative value for left, positive value for right. |
| `--in-operating` | Move the cursor only if it's currently waiting for an operation. |

### `backward`[​](#input.backward "Direct link to input.backward")

Move back to the start of the current or previous word.

### `forward`[​](#input.forward "Direct link to input.forward")

Move forward to the start of the next word.

| Argument/Option | Description |
| --- | --- |
| `--end-of-word` | Move forward to the end of the current or next word. |

### `insert`[​](#input.insert "Direct link to input.insert")

Enter insert mode. This command is only available in normal mode.

| Argument/Option | Description |
| --- | --- |
| `--append` | Insert after the cursor. |

### `visual`[​](#input.visual "Direct link to input.visual")

Enter visual mode. This command is only available in normal mode.

### `delete`[​](#input.delete "Direct link to input.delete")

Delete the selected characters. This command is only available in normal mode.

| Argument/Option | Description |
| --- | --- |
| `--cut` | Cut the selected characters into clipboard, instead of only deleting them. |
| `--insert` | Delete and enter insert mode. |

### `yank`[​](#input.yank "Direct link to input.yank")

Copy the selected characters. This command is only available in normal mode.

### `paste`[​](#input.paste "Direct link to input.paste")

Paste the copied characters after the cursor. This command is only available in normal mode.

| Argument/Option | Description |
| --- | --- |
| `--before` | Paste the copied characters before the cursor. |

### `undo`[​](#input.undo "Direct link to input.undo")

Undo the last operation. This command is only available in normal mode.

### `redo`[​](#input.redo "Direct link to input.redo")

Redo the last operation. This command is only available in normal mode.

### `help`[​](#input.help "Direct link to input.help")

Open the help menu. This command is only available in normal mode.

### `backspace`[​](#input.backspace "Direct link to input.backspace")

Delete the character before the cursor. This command is only available in insert mode.

| Argument/Option | Description |
| --- | --- |
| `--under` | Delete the character under the cursor. |

### `kill`[​](#input.kill "Direct link to input.kill")

Kill the specified range of characters. This command is only available in insert mode.

| Argument/Option | Description |
| --- | --- |
| `"bol"` | Kill backwards to the BOL. |
| `"eol"` | Kill forwards to the EOL. |
| `"backward"` | Kill backwards to the start of the current word. |
| `"forward"` | Kill forwards to the end of the current word. |

### `plugin`[​](#input.plugin "Direct link to input.plugin")

See [Functional plugin](/docs/plugins/overview#functional-plugin). This command is only available in normal mode.

### `noop`[​](#input.noop "Direct link to input.noop")

See [`noop` command](#mgr.noop).

## [confirm][​](#confirm "Direct link to [confirm]")

### `close`[​](#confirm.close "Direct link to confirm.close")

Cancel and close the confirmation dialog.

| Argument/Option | Description |
| --- | --- |
| `--submit` | Submit the confirmation. |

### `arrow`[​](#confirm.arrow "Direct link to confirm.arrow")

| Argument/Option | Description |
| --- | --- |
| `[steps]` | The number of steps the cursor moves up or down. |

`[steps]` can be one of the following values:

| Value | Description |
| --- | --- |
| `n` | Move the cursor `n` lines up or down, negative for up, positive for down. |
| `n%` | Move the cursor `n%` of the screen height up or down, negative for up, positive for down. |
| `"top"` | Move the cursor to the top (first item). |
| `"bot"` | Move the cursor to the bottom (last item). |
| `"prev"` | Go to the previous item, or the bottom if the cursor is at the top. |
| `"next"` | Go to the next item, or the top if the cursor is at the bottom. |

The `arrow prev`/`arrow next` commands are similar to `arrow -1`/`arrow 1`, except that the former supports wraparound scrolling.

### `help`[​](#confirm.help "Direct link to confirm.help")

Open the help menu.

## [cmp][​](#cmp "Direct link to [cmp]")

### `close`[​](#cmp.close "Direct link to cmp.close")

Hide the completion menu.

| Argument/Option | Description |
| --- | --- |
| `--submit` | Submit the completion. |

### `arrow`[​](#cmp.arrow "Direct link to cmp.arrow")

| Argument/Option | Description |
| --- | --- |
| `[steps]` | The number of steps the cursor moves up or down. |

`[steps]` can be one of the following values:

| Value | Description |
| --- | --- |
| `n` | Move the cursor `n` lines up or down, negative for up, positive for down. |
| `n%` | Move the cursor `n%` of the screen height up or down, negative for up, positive for down. |
| `"top"` | Move the cursor to the top (first item). |
| `"bot"` | Move the cursor to the bottom (last item). |
| `"prev"` | Go to the previous item, or the bottom if the cursor is at the top. |
| `"next"` | Go to the next item, or the top if the cursor is at the bottom. |

The `arrow prev`/`arrow next` commands are similar to `arrow -1`/`arrow 1`, except that the former supports wraparound scrolling.

### `help`[​](#cmp.help "Direct link to cmp.help")

Open the help menu.

### `plugin`[​](#cmp.plugin "Direct link to cmp.plugin")

See [Functional plugin](/docs/plugins/overview#functional-plugin).

### `noop`[​](#cmp.noop "Direct link to cmp.noop")

See [`noop` command](#mgr.noop).

## [help][​](#help "Direct link to [help]")

### `close`[​](#help.close "Direct link to help.close")

Hide the help menu.

### `escape`[​](#help.escape "Direct link to help.escape")

Clear the filter, or hide the help menu.

### `arrow`[​](#help.arrow "Direct link to help.arrow")

| Argument/Option | Description |
| --- | --- |
| `[steps]` | The number of steps the cursor moves up or down. |

`[steps]` can be one of the following values:

| Value | Description |
| --- | --- |
| `n` | Move the cursor `n` lines up or down, negative for up, positive for down. |
| `n%` | Move the cursor `n%` of the screen height up or down, negative for up, positive for down. |
| `"top"` | Move the cursor to the top (first item). |
| `"bot"` | Move the cursor to the bottom (last item). |
| `"prev"` | Go to the previous item, or the bottom if the cursor is at the top. |
| `"next"` | Go to the next item, or the top if the cursor is at the bottom. |

The `arrow prev`/`arrow next` commands are similar to `arrow -1`/`arrow 1`, except that the former supports wraparound scrolling.

### `filter`[​](#help.filter "Direct link to help.filter")

Apply a filter for the help items.

### `plugin`[​](#help.plugin "Direct link to help.plugin")

See [Functional plugin](/docs/plugins/overview#functional-plugin).

### `noop`[​](#help.noop "Direct link to help.noop")

See [`noop` command](#mgr.noop).
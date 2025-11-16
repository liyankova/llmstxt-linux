---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/choose-files/"
title: "Selecting files, fast - kitty"
crawl_date: "2025-11-16T14:48:46.772905Z"
selector: "article"
---

# Selecting files, fast - kitty

# Selecting files, fast[¶](#selecting-files-fast "Link to this heading")

Added in version 0.43.0.

The choose-files kitten is designed to allow you to select files, very fast,
with just a few key strokes. It operates like [fzf](https://github.com/junegunn/fzf/) and similar fuzzy finders, except that
it is specialised for finding files. As such it supports features such as
filtering by file type, file type icons, content previews and
so on, out of the box. It can be used as a drop in (but much more efficient and
keyboard friendly) replacement for the File open and save
dialog boxes common to GUI programs. On Linux, with the help of the
[desktop-ui](../desktop-ui/) kitten, you can even convince
most GUI programs on your computer to use this kitten instead of regular file
dialogs.

Simply run it as:

```
kitten choose-files
```

to select a single file from the tree rooted at the current working directory.
Type a few letters from the filename and once it becomes the top selection,
press `Enter`. You can change the current directory by instead selecting a
directory and pressing the `Tab` key. `Shift`+`Tab` goes up one
directory level.

## Creating shortcuts to favorite/frequently used directories[¶](#creating-shortcuts-to-favorite-frequently-used-directories "Link to this heading")

You can create keyboard shortcuts to quickly switch to any directory in
`choose-files.conf`. For example:

```
map ctrl+t cd /tmp
map alt+p  cd ~/my/project
```

## Selecting multiple files[¶](#selecting-multiple-files "Link to this heading")

When you wish to select multiple files, start the kitten with [`--mode`](#cmdoption-kitty-kitten-choose_files-mode)`=files`. Then instead of pressing
`Enter`, press `Shift`+`Enter` instead and the file will be added to the list
of selections. You can also hold the `Ctrl` key and click on files to add
them to the selections. Similarly, you can hold the `Alt` key and click to
select ranges of files (similar to using `Shift`+`click` in a GUI app).
Press `Enter` on the last selected file to finish. The list of selected
files is displayed at the bottom of the kitten and you can click on them
to deselect a file. Similarly, pressing `Shift`+`Enter` will un-select a
previously selected file.

## Hidden and ignored files[¶](#hidden-and-ignored-files "Link to this heading")

By default, the kitten does not process hidden files and directories (whose
names start with a period). This can be [`changed in the configuration`](#opt-kitten-choose_files.show_hidden)
and also at runtime via the clickable link to the right of the search input.

Similarly, the kitten respects both `.gitignore` and `.ignore`
files, by default. This can also be changed both [`in configuration`](#opt-kitten-choose_files.respect_ignores) or at runtime. Note that
`.gitignore` files are only respected if there is also a `.git`
directory present. The kitten also supports the global `.gitignore` file,
though it applies only inside git working trees. You can specify [`global ignore
patterns`](#opt-kitten-choose_files.ignore), that apply everywhere in `choose-files.conf`.

## Selecting non-existent files (save file names)[¶](#selecting-non-existent-files-save-file-names "Link to this heading")

This kitten can also be used to select non-existent files, that is a new file
for a Save file type of dialog using [`--mode`](#cmdoption-kitty-kitten-choose_files-mode)`=save-file`. Once you have changed to the directory
you want the file to be in (using the `Tab` key),
press `Ctrl`+`Enter` and you will be able to type in the file name.

## Selecting directories[¶](#selecting-directories "Link to this heading")

This kitten can also be used to select directories,
for an Open directory type of dialog using [`--mode`](#cmdoption-kitty-kitten-choose_files-mode)`=dir`. Once you have changed to the directory
you want, press `Ctrl`+`Enter` to accept it. Or if you are in a parent
directory you can select a descendant directory by pressing `Enter`, the
same as you would for selecting a file to open.

## Configuration[¶](#configuration "Link to this heading")

You can configure various aspects of the kitten’s operation by creating a
`choose-files.conf` in your [kitty config folder](../../conf/#confloc).
See below for the supported configuration directives.

## Filesystem scanning[¶](#filesystem-scanning "Link to this heading")

show\_hidden[¶](#opt-kitten-choose_files.show_hidden "Link to this definition")

```
show_hidden last
```

Whether to show hidden files. The default value of `last` means remember the last
used value. This setting can be toggled withing the program.

sort\_by\_last\_modified[¶](#opt-kitten-choose_files.sort_by_last_modified "Link to this definition")

```
sort_by_last_modified last
```

Whether to sort the list of entries by last modified, instead of name. Note that sorting only applies
before any query is entered. Once a query is entered entries are sorted by their matching score.
The default value of `last` means remember the last
used value. This setting can be toggled withing the program.

respect\_ignores[¶](#opt-kitten-choose_files.respect_ignores "Link to this definition")

```
respect_ignores last
```

Whether to respect .gitignore and .ignore files and the [`ignore`](#opt-kitten-choose_files.ignore) setting.
The default value of `last` means remember the last used value.
This setting can be toggled withing the program.

ignore[¶](#opt-kitten-choose_files.ignore "Link to this definition")

An ignore pattern to ignore matched files. Uses the same sytax as `.gitignore` files (see `man gitignore`).
Anchored patterns match with respect to whatever directory is currently being displayed.
Can be specified multiple times to use multiple patterns. Note that every pattern
has to be checked against every file, so use sparingly.

## Appearance[¶](#appearance "Link to this heading")

show\_preview[¶](#opt-kitten-choose_files.show_preview "Link to this definition")

```
show_preview last
```

Whether to show a preview of the current file/directory. The default value of `last` means remember the last
used value. This setting can be toggled withing the program.

pygments\_style[¶](#opt-kitten-choose_files.pygments_style "Link to this definition")

```
pygments_style default
```

The pygments color scheme to use for syntax highlighting of file previews. See [pygments builtin styles](https://pygments.org/styles/) for a list of schemes.
This sets the colors used for light color schemes, use [`dark_pygments_style`](#opt-kitten-choose_files.dark_pygments_style) to change the
colors for dark color schemes.

dark\_pygments\_style[¶](#opt-kitten-choose_files.dark_pygments_style "Link to this definition")

```
dark_pygments_style github-dark
```

The pygments color scheme to use for syntax highlighting with dark colors. See [pygments builtin styles](https://pygments.org/styles/) for a list of schemes.
This sets the colors used for dark color schemes, use [`pygments_style`](#opt-kitten-choose_files.pygments_style) to change the
colors for light color schemes.

cache\_size[¶](#opt-kitten-choose_files.cache_size "Link to this definition")

```
cache_size 0.5
```

The maximum size of the disk cache, in gigabytes, used for previews. Zero or negative values
mean no limit.

syntax\_aliases[¶](#opt-kitten-choose_files.syntax_aliases "Link to this definition")

```
syntax_aliases pyj:py pyi:py recipe:py
```

File extension aliases for syntax highlight. For example, to syntax highlight
`file.xyz` as `file.abc` use a setting of `xyz:abc`.
Multiple aliases must be separated by spaces.

## Keyboard shortcuts[¶](#keyboard-shortcuts "Link to this heading")

Quit[¶](#shortcut-kitten-choose_files.Quit "Link to this definition")

```
map esc quit
map ctrl+c quit
```

Accept current result[¶](#shortcut-kitten-choose_files.Accept-current-result "Link to this definition")

```
map enter accept
```

Select current result[¶](#shortcut-kitten-choose_files.Select-current-result "Link to this definition")

```
map shift+enter select
```

When selecting multiple files, this will add the current file to the list of selected files.
You can also toggle the selected status of a file by holding down the `Ctrl` key and clicking on
it. Similarly, the `Alt` key can be held to click and extend the range of selected files.

Type file name[¶](#shortcut-kitten-choose_files.Type-file-name "Link to this definition")

```
map ctrl+enter typename
```

Type a file name/path rather than filtering the list of existing files.
Useful when specifying a file or directory name for saving that does not yet exist.
When choosing existing directories, will accept the directory whoose
contents are being currently displayed as the choice.
Does not work when selecting files to open rather than to save.

Next result[¶](#shortcut-kitten-choose_files.Next-result "Link to this definition")

```
map down next 1
```

Previous result[¶](#shortcut-kitten-choose_files.Previous-result "Link to this definition")

```
map up next -1
```

Left result[¶](#shortcut-kitten-choose_files.Left-result "Link to this definition")

```
map left next left
```

Right result[¶](#shortcut-kitten-choose_files.Right-result "Link to this definition")

```
map right next right
```

First result on screen[¶](#shortcut-kitten-choose_files.First-result-on-screen "Link to this definition")

```
map home next first_on_screen
map ctrl+home next first
```

Last result on screen[¶](#shortcut-kitten-choose_files.Last-result-on-screen "Link to this definition")

```
map end next last_on_screen
map ctrl+end next last
```

Change to currently selected dir[¶](#shortcut-kitten-choose_files.Change-to-currently-selected-dir "Link to this definition")

```
map tab cd .
```

Change to parent directory[¶](#shortcut-kitten-choose_files.Change-to-parent-directory "Link to this definition")

```
map shift+tab cd ..
```

Change to root directory[¶](#shortcut-kitten-choose_files.Change-to-root-directory "Link to this definition")

```
map ctrl+/ cd /
```

Change to home directory[¶](#shortcut-kitten-choose_files.Change-to-home-directory "Link to this definition")

```
map ctrl+~ cd ~
map ctrl+` cd ~
map ctrl+shift+` cd ~
```

Change to temp directory[¶](#shortcut-kitten-choose_files.Change-to-temp-directory "Link to this definition")

```
map ctrl+t cd /tmp
```

Next filter[¶](#shortcut-kitten-choose_files.Next-filter "Link to this definition")

```
map ctrl+f 1
```

Previous filter[¶](#shortcut-kitten-choose_files.Previous-filter "Link to this definition")

```
map alt+f -1
```

Toggle showing dotfiles[¶](#shortcut-kitten-choose_files.Toggle-showing-dotfiles "Link to this definition")

```
map alt+h toggle dotfiles
```

Toggle showing ignored files[¶](#shortcut-kitten-choose_files.Toggle-showing-ignored-files "Link to this definition")

```
map alt+i toggle ignorefiles
```

Toggle sorting by dates[¶](#shortcut-kitten-choose_files.Toggle-sorting-by-dates "Link to this definition")

```
map alt+d toggle sort_by_dates
```

Toggle showing preview[¶](#shortcut-kitten-choose_files.Toggle-showing-preview "Link to this definition")

```
map alt+p toggle preview
```

## Source code for choose\_files[¶](#source-code-for-choose-files "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/choose_files).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten choose_files [options] [directory to start choosing files in]
```

Select one or more files, quickly, using fuzzy finding, by typing just a few characters from
the file name. Browse matching files, using the arrow keys to navigate matches and press `Enter`
to select. The `Tab` key can be used to change to a sub-folder. See the [online docs](#)
for full details.

### Options[¶](#options "Link to this heading")

--mode <MODE>[¶](#cmdoption-kitty-kitten-choose_files-mode "Link to this definition")
:   The type of object(s) to select
    Default: `file`
    Choices: `dir`, `dirs`, `file`, `files`, `save-dir`, `save-file`, `save-files`

--file-filter <FILE\_FILTER>[¶](#cmdoption-kitty-kitten-choose_files-file-filter "Link to this definition")
:   A list of filters to restrict the displayed files. Can be either mimetypes, or glob style patterns. Can be specified multiple times. The syntax is `type:expression:Descriptive Name`. For example: `mime:image/png:Images` and `mime:image/gif:Images` and `glob:*.[tT][xX][Tt]:Text files`. Note that glob patterns are case-sensitive. The mimetype specification is treated as a glob expressions as well, so you can, for example, use `mime:text/*` to match all text files. The first filter in the list will be applied by default. Use a filter such as `glob:*:All` to match all files. Note that filtering only appies to files, not directories.

--suggested-save-file-name <SUGGESTED\_SAVE\_FILE\_NAME>[¶](#cmdoption-kitty-kitten-choose_files-suggested-save-file-name "Link to this definition")
:   A suggested name when picking a save file.

--suggested-save-file-path <SUGGESTED\_SAVE\_FILE\_PATH>[¶](#cmdoption-kitty-kitten-choose_files-suggested-save-file-path "Link to this definition")
:   Path to an existing file to use as the save file.

--title <TITLE>[¶](#cmdoption-kitty-kitten-choose_files-title "Link to this definition")
:   Window title to use for this chooser

--display-title [=no][¶](#cmdoption-kitty-kitten-choose_files-display-title "Link to this definition")
:   Show the window title at the top, useful when this kitten is used in an OS window without a title bar.

--override <OVERRIDE>, -o <OVERRIDE>[¶](#cmdoption-kitty-kitten-choose_files-override "Link to this definition")
:   Override individual configuration options, can be specified multiple times. Syntax: name=value.

--config <CONFIG>[¶](#cmdoption-kitty-kitten-choose_files-config "Link to this definition")
:   Specify a path to the configuration file(s) to use. All configuration files are merged onto the builtin `choose-files.conf`, overriding the builtin values. This option can be specified multiple times to read multiple configuration files in sequence, which are merged. Use the special value `NONE` to not load any config file.

    If this option is not specified, config files are searched for in the order: `$XDG_CONFIG_HOME/kitty/choose-files.conf`, `~/.config/kitty/choose-files.conf`, `$XDG_CONFIG_DIRS/kitty/choose-files.conf`. The first one that exists is used as the config file.

    If the environment variable [`KITTY_CONFIG_DIRECTORY`](../../glossary/#envvar-KITTY_CONFIG_DIRECTORY) is specified, that directory is always used and the above searching does not happen.

    If `/etc/xdg/kitty/choose-files.conf` exists, it is merged before (i.e. with lower priority) than any user config files. It can be used to specify system-wide defaults for all users. You can use either `-` or `/dev/stdin` to read the config from STDIN.

--write-output-to <WRITE\_OUTPUT\_TO>[¶](#cmdoption-kitty-kitten-choose_files-write-output-to "Link to this definition")
:   Path to a file to which the output is written in addition to STDOUT.

--output-format <OUTPUT\_FORMAT>[¶](#cmdoption-kitty-kitten-choose_files-output-format "Link to this definition")
:   The format in which to write the output.
    Default: `text`
    Choices: `json`, `text`

--write-pid-to <WRITE\_PID\_TO>[¶](#cmdoption-kitty-kitten-choose_files-write-pid-to "Link to this definition")
:   Path to a file to which to write the process ID (PID) of this process to.
---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/diff/"
title: "kitty-diff - kitty"
crawl_date: "2025-11-16T14:48:17.806906Z"
selector: "article"
---

# kitty-diff - kitty

# kitty-diff[¶](#kitty-diff "Link to this heading")

*A fast side-by-side diff tool with syntax highlighting and images*

## Major Features[¶](#major-features "Link to this heading")

* Displays diffs side-by-side in the kitty terminal
* Does syntax highlighting of the displayed diffs, asynchronously, for
  maximum speed
* Displays images as well as text diffs, even over SSH
* Does recursive directory diffing

[![Screenshot, showing a sample diff](../../_images/diff.png)](../../_images/diff.png)

Screenshot, showing a sample diff[¶](#id1 "Link to this image")

## Installation[¶](#installation "Link to this heading")

Simply [install kitty](../../quickstart/#quickstart).

## Usage[¶](#usage "Link to this heading")

In the kitty terminal, run:

```
kitten diff file1 file2
```

to see the diff between `file1` and `file2`.

Create an alias in your shell’s startup file to shorten the command, for
example:

```
alias d="kitten diff"
```

Now all you need to do to diff two files is:

```
d file1 file2
```

You can also pass directories instead of files to see the recursive diff of the
directory contents.

## Keyboard controls[¶](#keyboard-controls "Link to this heading")

| Action | Shortcut |
| --- | --- |
| Quit | `Q` |
| Scroll line up | `K`, `Up` |
| Scroll line down | `J`, `Down` |
| Scroll page up | `PgUp` |
| Scroll page down | `PgDn` |
| Scroll to top | `Home` |
| Scroll to bottom | `End` |
| Scroll to next page | `Space`, `PgDn`, `Ctrl`+`F` |
| Scroll to previous page | `PgUp`, `Ctrl`+`B` |
| Scroll down half page | `Ctrl`+`D` |
| Scroll up half page | `Ctrl`+`U` |
| Scroll to next change | `N` |
| Scroll to previous change | `P` |
| Increase lines of context | `+` |
| Decrease lines of context | `-` |
| All lines of context | `A` |
| Restore default context | `=` |
| Search forwards | `/` |
| Search backwards | `?` |
| Clear search or exit | `Esc` |
| Scroll to next match | `>`, `.` |
| Scroll to previous match | `<`, `,` |
| Copy selection to clipboard | `y` |
| Copy selection or exit | `Ctrl`+`C` |

## Integrating with git[¶](#integrating-with-git "Link to this heading")

Add the following to `~/.gitconfig`:

```
[diff]
    tool = kitty
    guitool = kitty.gui
[difftool]
    prompt = false
    trustExitCode = true
[difftool "kitty"]
    cmd = kitten diff $LOCAL $REMOTE
[difftool "kitty.gui"]
    cmd = kitten diff $LOCAL $REMOTE
```

Now to use kitty-diff to view git diffs, you can simply do:

```
git difftool --no-symlinks --dir-diff
```

Once again, creating an alias for this command is useful.

## Why does this work only in kitty?[¶](#why-does-this-work-only-in-kitty "Link to this heading")

The diff kitten makes use of various features that are [kitty only](../../protocol-extensions/), such as the [kitty graphics protocol](../../graphics-protocol/), the [extended keyboard protocol](../../keyboard-protocol/), etc. It also leverages terminal program infrastructure
I created for all of kitty’s other kittens to reduce the amount of code needed
(the entire implementation is under 3000 lines of code).

And fundamentally, it’s kitty only because I wrote it for myself, and I am
highly unlikely to use any other terminals :)

## Configuration[¶](#configuration "Link to this heading")

You can configure the colors used, keyboard shortcuts, the diff implementation,
the default lines of context, etc. by creating a `diff.conf` file in your
[kitty config folder](../../conf/#confloc). See below for the supported configuration
directives.

## Diffing[¶](#diffing "Link to this heading")

syntax\_aliases[¶](#opt-kitten-diff.syntax_aliases "Link to this definition")

```
syntax_aliases pyj:py pyi:py recipe:py
```

File extension aliases for syntax highlight. For example, to syntax highlight
`file.xyz` as `file.abc` use a setting of `xyz:abc`.
Multiple aliases must be separated by spaces.

num\_context\_lines[¶](#opt-kitten-diff.num_context_lines "Link to this definition")

```
num_context_lines 3
```

The number of lines of context to show around each change.

diff\_cmd[¶](#opt-kitten-diff.diff_cmd "Link to this definition")

```
diff_cmd auto
```

The diff command to use. Must contain the placeholder `_CONTEXT_` which
will be replaced by the number of lines of context. A few special values are allowed:
`auto` will automatically pick an available diff implementation. `builtin`
will use the anchored diff algorithm from the Go standard library. `git` will
use the git command to do the diffing. `diff` will use the diff command to
do the diffing.

replace\_tab\_by[¶](#opt-kitten-diff.replace_tab_by "Link to this definition")

```
replace_tab_by \x20\x20\x20\x20
```

The string to replace tabs with. Default is to use four spaces.

ignore\_name[¶](#opt-kitten-diff.ignore_name "Link to this definition")

A glob pattern that is matched against only the filename of files and directories. Matching
files and directories are ignored when scanning the filesystem to look for files to diff.
Can be specified multiple times to use multiple patterns. For example:

```
ignore_name .git
ignore_name *~
ignore_name *.pyc
```

## Colors[¶](#colors "Link to this heading")

color\_scheme[¶](#opt-kitten-diff.color_scheme "Link to this definition")

```
color_scheme auto
```

Whether to use the light or dark colors. The default of `auto` means
to follow the parent terminal color scheme. Note that the actual colors used
for dark schemes are set by the `dark_*` settings below and the non-prefixed
settings are used for light colors.

pygments\_style[¶](#opt-kitten-diff.pygments_style "Link to this definition")

```
pygments_style default
```

The pygments color scheme to use for syntax highlighting. See [pygments builtin styles](https://pygments.org/styles/) for a list of schemes. Note that
this **does not** change the colors used for diffing,
only the colors used for syntax highlighting. To change the general colors use the settings below.
This sets the colors used for light color schemes, use [`dark_pygments_style`](#opt-kitten-diff.dark_pygments_style) to change the
colors for dark color schemes.

dark\_pygments\_style[¶](#opt-kitten-diff.dark_pygments_style "Link to this definition")

```
dark_pygments_style github-dark
```

The pygments color scheme to use for syntax highlighting with dark colors. See [pygments builtin styles](https://pygments.org/styles/) for a list of schemes. Note that
this **does not** change the colors used for diffing,
only the colors used for syntax highlighting. To change the general colors use the settings below.
This sets the colors used for dark color schemes, use [`pygments_style`](#opt-kitten-diff.pygments_style) to change the
colors for light color schemes.

foreground, dark\_foreground, background, dark\_background[¶](#opt-kitten-diff.foreground "Link to this definition")

```
foreground      black
dark_foreground #f8f8f2
background      white
dark_background #212830
```

Basic colors

title\_fg, dark\_title\_fg, title\_bg, dark\_title\_bg[¶](#opt-kitten-diff.title_fg "Link to this definition")

```
title_fg      black
dark_title_fg white
title_bg      white
dark_title_bg #212830
```

Title colors

margin\_bg, dark\_margin\_bg, margin\_fg, dark\_margin\_fg[¶](#opt-kitten-diff.margin_bg "Link to this definition")

```
margin_bg      #fafbfc
dark_margin_bg #212830
margin_fg      #aaaaaa
dark_margin_fg #aaaaaa
```

Margin colors

removed\_bg, dark\_removed\_bg, highlight\_removed\_bg, dark\_highlight\_removed\_bg, removed\_margin\_bg, dark\_removed\_margin\_bg[¶](#opt-kitten-diff.removed_bg "Link to this definition")

```
removed_bg                #ffeef0
dark_removed_bg           #352c33
highlight_removed_bg      #fdb8c0
dark_highlight_removed_bg #5c3539
removed_margin_bg         #ffdce0
dark_removed_margin_bg    #5c3539
```

Removed text backgrounds

added\_bg, dark\_added\_bg, highlight\_added\_bg, dark\_highlight\_added\_bg, added\_margin\_bg, dark\_added\_margin\_bg[¶](#opt-kitten-diff.added_bg "Link to this definition")

```
added_bg                #e6ffed
dark_added_bg           #263834
highlight_added_bg      #acf2bd
dark_highlight_added_bg #31503d
added_margin_bg         #cdffd8
dark_added_margin_bg    #31503d
```

Added text backgrounds

filler\_bg, dark\_filler\_bg[¶](#opt-kitten-diff.filler_bg "Link to this definition")

```
filler_bg      #fafbfc
dark_filler_bg #262c36
```

Filler (empty) line background

margin\_filler\_bg, dark\_margin\_filler\_bg[¶](#opt-kitten-diff.margin_filler_bg "Link to this definition")

```
margin_filler_bg      none
dark_margin_filler_bg none
```

Filler (empty) line background in margins, defaults to the filler background

hunk\_margin\_bg, dark\_hunk\_margin\_bg, hunk\_bg, dark\_hunk\_bg[¶](#opt-kitten-diff.hunk_margin_bg "Link to this definition")

```
hunk_margin_bg      #dbedff
dark_hunk_margin_bg #0c2d6b
hunk_bg             #f1f8ff
dark_hunk_bg        #253142
```

Hunk header colors

search\_bg, dark\_search\_bg, search\_fg, dark\_search\_fg, select\_bg, dark\_select\_bg, select\_fg, dark\_select\_fg[¶](#opt-kitten-diff.search_bg "Link to this definition")

```
search_bg      #444
dark_search_bg #2c599c
search_fg      white
dark_search_fg white
select_bg      #b4d5fe
dark_select_bg #2c599c
select_fg      black
dark_select_fg white
```

Highlighting

## Keyboard shortcuts[¶](#keyboard-shortcuts "Link to this heading")

Quit[¶](#shortcut-kitten-diff.Quit "Link to this definition")

```
map q quit
map esc quit
```

Scroll down[¶](#shortcut-kitten-diff.Scroll-down "Link to this definition")

```
map j scroll_by 1
map down scroll_by 1
```

Scroll up[¶](#shortcut-kitten-diff.Scroll-up "Link to this definition")

```
map k scroll_by -1
map up scroll_by -1
```

Scroll to top[¶](#shortcut-kitten-diff.Scroll-to-top "Link to this definition")

```
map home scroll_to start
```

Scroll to bottom[¶](#shortcut-kitten-diff.Scroll-to-bottom "Link to this definition")

```
map end scroll_to end
```

Scroll to next page[¶](#shortcut-kitten-diff.Scroll-to-next-page "Link to this definition")

```
map page_down scroll_to next-page
map space scroll_to next-page
map ctrl+f scroll_to next-page
```

Scroll to previous page[¶](#shortcut-kitten-diff.Scroll-to-previous-page "Link to this definition")

```
map page_up scroll_to prev-page
map ctrl+b scroll_to prev-page
```

Scroll down half page[¶](#shortcut-kitten-diff.Scroll-down-half-page "Link to this definition")

```
map ctrl+d scroll_to next-half-page
```

Scroll up half page[¶](#shortcut-kitten-diff.Scroll-up-half-page "Link to this definition")

```
map ctrl+u scroll_to prev-half-page
```

Scroll to next change[¶](#shortcut-kitten-diff.Scroll-to-next-change "Link to this definition")

```
map n scroll_to next-change
```

Scroll to previous change[¶](#shortcut-kitten-diff.Scroll-to-previous-change "Link to this definition")

```
map p scroll_to prev-change
```

Scroll to next file[¶](#shortcut-kitten-diff.Scroll-to-next-file "Link to this definition")

```
map shift+j scroll_to next-file
```

Scroll to previous file[¶](#shortcut-kitten-diff.Scroll-to-previous-file "Link to this definition")

```
map shift+k scroll_to prev-file
```

Show all context[¶](#shortcut-kitten-diff.Show-all-context "Link to this definition")

```
map a change_context all
```

Show default context[¶](#shortcut-kitten-diff.Show-default-context "Link to this definition")

```
map = change_context default
```

Increase context[¶](#shortcut-kitten-diff.Increase-context "Link to this definition")

```
map + change_context 5
```

Decrease context[¶](#shortcut-kitten-diff.Decrease-context "Link to this definition")

```
map - change_context -5
```

Search forward[¶](#shortcut-kitten-diff.Search-forward "Link to this definition")

```
map / start_search regex forward
```

Search backward[¶](#shortcut-kitten-diff.Search-backward "Link to this definition")

```
map ? start_search regex backward
```

Scroll to next search match[¶](#shortcut-kitten-diff.Scroll-to-next-search-match "Link to this definition")

```
map . scroll_to next-match
map > scroll_to next-match
```

Scroll to previous search match[¶](#shortcut-kitten-diff.Scroll-to-previous-search-match "Link to this definition")

```
map , scroll_to prev-match
map < scroll_to prev-match
```

Search forward (no regex)[¶](#shortcut-kitten-diff.Search-forward-no-regex "Link to this definition")

```
map f start_search substring forward
```

Search backward (no regex)[¶](#shortcut-kitten-diff.Search-backward-no-regex "Link to this definition")

```
map b start_search substring backward
```

Copy selection to clipboard[¶](#shortcut-kitten-diff.Copy-selection-to-clipboard "Link to this definition")

```
map y copy_to_clipboard
```

Copy selection to clipboard or exit if no selection is present[¶](#shortcut-kitten-diff.Copy-selection-to-clipboard-or-exit-if-no-selection-is-present "Link to this definition")

```
map ctrl+c copy_to_clipboard_or_exit
```

## Source code for diff[¶](#source-code-for-diff "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/diff).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten diff [options] file_or_directory_left file_or_directory_right
```

Show a side-by-side diff of the specified files/directories. You can also use ssh:hostname:remote-file-path to diff remote files.

### Options[¶](#options "Link to this heading")

--context <CONTEXT>[¶](#cmdoption-kitty-kitten-diff-context "Link to this definition")
:   Number of lines of context to show between changes. Negative values use the number set in `diff.conf`.
    Default: `-1`

--config <CONFIG>[¶](#cmdoption-kitty-kitten-diff-config "Link to this definition")
:   Specify a path to the configuration file(s) to use. All configuration files are merged onto the builtin `diff.conf`, overriding the builtin values. This option can be specified multiple times to read multiple configuration files in sequence, which are merged. Use the special value `NONE` to not load any config file.

    If this option is not specified, config files are searched for in the order: `$XDG_CONFIG_HOME/kitty/diff.conf`, `~/.config/kitty/diff.conf`, `$XDG_CONFIG_DIRS/kitty/diff.conf`. The first one that exists is used as the config file.

    If the environment variable [`KITTY_CONFIG_DIRECTORY`](../../glossary/#envvar-KITTY_CONFIG_DIRECTORY) is specified, that directory is always used and the above searching does not happen.

    If `/etc/xdg/kitty/diff.conf` exists, it is merged before (i.e. with lower priority) than any user config files. It can be used to specify system-wide defaults for all users. You can use either `-` or `/dev/stdin` to read the config from STDIN.

--override <OVERRIDE>, -o <OVERRIDE>[¶](#cmdoption-kitty-kitten-diff-override "Link to this definition")
:   Override individual configuration options, can be specified multiple times. Syntax: name=value. For example: -o background=gray

## Sample diff.conf[¶](#sample-diff-conf "Link to this heading")

You can download a sample `diff.conf` file with all default settings and
comments describing each setting by clicking: [`sample diff.conf`](../../_downloads/a489ebbb52d84eeb19a12b2fda7debda/diff.conf).
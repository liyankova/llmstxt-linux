---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/hints/"
title: "Hints - kitty"
crawl_date: "2025-11-16T14:48:24.767821Z"
selector: "article"
---

# Hints - kitty

# Hints[¶](#hints "Link to this heading")

*kitty* has a *hints mode* to select and act on arbitrary text snippets
currently visible on the screen. For example, you can press [`ctrl+shift+e`](../../conf/#shortcut-kitty.Open-URL)
to choose any URL visible on the screen and then open it using your default web
browser.

[![URL hints mode](../../_images/hints_mode.png)](../../_images/hints_mode.png)

URL hints mode[¶](#id1 "Link to this image")

Similarly, you can press [`ctrl+shift+p>f`](../../conf/#shortcut-kitty.Insert-selected-path) to select anything that
looks like a path or filename and then insert it into the terminal, very useful
for picking files from the output of a **git** or **ls** command
and adding them to the command line for the next command.

You can also press [`ctrl+shift+p>n`](../../conf/#shortcut-kitty.Open-the-selected-file-at-the-selected-line) to select anything that looks like a
path or filename followed by a colon and a line number and open the file in
your default editor at the specified line number (opening at line number will
work only if your editor supports the +linenum command line syntax or is a
“known” editor). The patterns and editor to be used can be modified using
options passed to the kitten. For example:

```
map ctrl+g kitten hints --type=linenum --linenum-action=tab nvim +{line} {path}
```

will open the selected file in a new tab inside [Neovim](https://neovim.io/)
when you press `Ctrl`+`G`.

Pressing [`ctrl+shift+p>y`](../../conf/#shortcut-kitty.Open-the-selected-hyperlink) will open [hyperlinks](../../glossary/#term-hyperlinks), i.e. a URL
that has been marked as such by the program running in the terminal,
for example, by `ls --hyperlink=auto`. If **ls** comes with your OS
does not support hyperlink, you may need to install [GNU Coreutils](https://www.gnu.org/software/coreutils/).

You can also [customize what actions are taken for different types of URLs](../../open_actions/).

Note

If there are more hints than letters, hints will use multiple
letters. In this case, when you press the first letter, only hints
starting with that letter are displayed. Pressing the second letter will
select that hint or press `Enter` or `Space` to select the empty
hint.

For mouse lovers, the hints kitten also allows you to click on any matched text to
select it instead of typing the hint character.

The hints kitten is very powerful to see more detailed help on its various
options and modes of operation, see below. You can use these options to
create mappings in `kitty.conf` to select various different text
snippets. See [`insert_selected_path`](../../conf/#shortcut-kitty.Insert-selected-path) for examples.

## Completely customizing the matching and actions of the kitten[¶](#completely-customizing-the-matching-and-actions-of-the-kitten "Link to this heading")

The hints kitten supports writing simple Python scripts that can be used to
completely customize how it finds matches and what happens when a match is
selected. This allows the hints kitten to provide the user interface, while you
can provide the logic for finding matches and performing actions on them. This
is best illustrated with an example. Create the file `custom-hints.py` in
the [kitty config directory](../../conf/#confloc) with the following contents:

```
import re

def mark(text, args, Mark, extra_cli_args, *a):
    # This function is responsible for finding all
    # matching text. extra_cli_args are any extra arguments
    # passed on the command line when invoking the kitten.
    # We mark all individual word for potential selection
    for idx, m in enumerate(re.finditer(r'\w+', text)):
        start, end = m.span()
        mark_text = text[start:end].replace('\n', '').replace('\0', '')
        # The empty dictionary below will be available as groupdicts
        # in handle_result() and can contain string keys and arbitrary JSON
        # serializable values.
        yield Mark(idx, start, end, mark_text, {})

def handle_result(args, data, target_window_id, boss, extra_cli_args, *a):
    # This function is responsible for performing some
    # action on the selected text.
    # matches is a list of the selected entries and groupdicts contains
    # the arbitrary data associated with each entry in mark() above
    matches, groupdicts = [], []
    for m, g in zip(data['match'], data['groupdicts']):
        if m:
            matches.append(m), groupdicts.append(g)
    for word, match_data in zip(matches, groupdicts):
        # Lookup the word in a dictionary, the open_url function
        # will open the provided url in the system browser
        boss.open_url(f'https://www.google.com/search?q=define:{word}')
```

Now run kitty with:

```
kitty -o 'map f1 kitten hints --customize-processing custom-hints.py'
```

When you press the `F1` key you will be able to select a word to
look it up in the Google dictionary.

## Source code for hints[¶](#source-code-for-hints "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/hints).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten hints [options]
```

Select text from the screen using the keyboard. Defaults to searching for URLs.

### Options[¶](#options "Link to this heading")

--program <PROGRAM>[¶](#cmdoption-kitty-kitten-hints-program "Link to this definition")
:   What program to use to open matched text. Defaults to the default open program for the operating system. Various special values are supported:

    `-`
    :   paste the match into the terminal window.

    `@`
    :   copy the match to the clipboard

    `*`
    :   copy the match to the primary selection (on systems that support primary selections)

    `@NAME`
    :   copy the match to the specified buffer, e.g. `@a`

    `default`
    :   run the default open program. Note that when using the hyperlink `--type` the default is to use the kitty [hyperlink handling](../../open_actions/) facilities.

    `launch`
    :   run [The launch command](../../launch/) to open the program in a new kitty tab, window, overlay, etc. For example:

        ```
        --program "launch --type=tab vim"
        ```

    Can be specified multiple times to run multiple programs.

--type <TYPE>[¶](#cmdoption-kitty-kitten-hints-type "Link to this definition")
:   The type of text to search for. A value of `linenum` is special, it looks for error messages using the pattern specified with [`--regex`](#cmdoption-kitty-kitten-hints-regex), which must have the named groups: `path` and `line`. If not specified, will look for `path:line`. The [`--linenum-action`](#cmdoption-kitty-kitten-hints-linenum-action) option controls where to display the selected error message, other options are ignored.
    Default: `url`
    Choices: `hash`, `hyperlink`, `ip`, `line`, `linenum`, `path`, `regex`, `url`, `word`

--regex <REGEX>[¶](#cmdoption-kitty-kitten-hints-regex "Link to this definition")
:   The regular expression to use when option [`--type`](#cmdoption-kitty-kitten-hints-type) is set to `regex`, in Perl 5 syntax. If you specify a numbered group in the regular expression, only the group will be matched. This allows you to match text ignoring a prefix/suffix, as needed. The default expression matches lines. To match text over multiple lines, things get a little tricky, as line endings are a sequence of zero or more null bytes followed by either a carriage return or a newline character. To have a pattern match over line endings you will need to match the character set `[\0\r\n]`. The newlines and null bytes are automatically stripped from the returned text. If you specify named groups and a [`--program`](#cmdoption-kitty-kitten-hints-program), then the program will be passed arguments corresponding to each named group of the form `key=value`.
    Default: `(?m)^\s*(.+?)\s*$`

--linenum-action <LINENUM\_ACTION>[¶](#cmdoption-kitty-kitten-hints-linenum-action "Link to this definition")
:   Where to perform the action on matched errors. `self` means the current window, `window` a new kitty window, `tab` a new tab, `os_window` a new OS window and `background` run in the background. `remote-control` is like background but the program can use kitty remote control without needing to turn on remote control globally. The actual action is whatever arguments are provided to the kitten, for example: `kitten hints --type=linenum --linenum-action=tab vim +{line} {path}` will open the matched path at the matched line number in vim in a new kitty tab. Note that in order to use [`--program`](#cmdoption-kitty-kitten-hints-program) to copy or paste the provided arguments, you need to use the special value `self`.
    Default: `self`
    Choices: `background`, `os_window`, `remote-control`, `self`, `tab`, `window`

--url-prefixes <URL\_PREFIXES>[¶](#cmdoption-kitty-kitten-hints-url-prefixes "Link to this definition")
:   Comma separated list of recognized URL prefixes. Defaults to the list of prefixes defined by the [`url_prefixes`](../../conf/#opt-kitty.url_prefixes) option in `kitty.conf`.
    Default: `default`

--url-excluded-characters <URL\_EXCLUDED\_CHARACTERS>[¶](#cmdoption-kitty-kitten-hints-url-excluded-characters "Link to this definition")
:   Characters to exclude when matching URLs. Defaults to the list of characters defined by the [`url_excluded_characters`](../../conf/#opt-kitty.url_excluded_characters) option in `kitty.conf`. The syntax for this option is the same as for [`url_excluded_characters`](../../conf/#opt-kitty.url_excluded_characters).
    Default: `default`

--word-characters <WORD\_CHARACTERS>[¶](#cmdoption-kitty-kitten-hints-word-characters "Link to this definition")
:   Characters to consider as part of a word. In addition, all characters marked as alphanumeric in the Unicode database will be considered as word characters. Defaults to the [`select_by_word_characters`](../../conf/#opt-kitty.select_by_word_characters) option from `kitty.conf`.

--minimum-match-length <MINIMUM\_MATCH\_LENGTH>[¶](#cmdoption-kitty-kitten-hints-minimum-match-length "Link to this definition")
:   The minimum number of characters to consider a match.
    Default: `3`

--multiple [=no][¶](#cmdoption-kitty-kitten-hints-multiple "Link to this definition")
:   Select multiple matches and perform the action on all of them together at the end. In this mode, press `Esc` to finish selecting.

--multiple-joiner <MULTIPLE\_JOINER>[¶](#cmdoption-kitty-kitten-hints-multiple-joiner "Link to this definition")
:   String for joining multiple selections when copying to the clipboard or inserting into the terminal. The special values are: `space` - a space character, `newline` - a newline, `empty` - an empty joiner, `json` - a JSON serialized list, `auto` - an automatic choice, based on the type of text being selected. In addition, integers are interpreted as zero-based indices into the list of selections. You can use `0` for the first selection and `-1` for the last.
    Default: `auto`

--add-trailing-space <ADD\_TRAILING\_SPACE>[¶](#cmdoption-kitty-kitten-hints-add-trailing-space "Link to this definition")
:   Add trailing space after matched text. Defaults to `auto`, which adds the space when used together with [`--multiple`](#cmdoption-kitty-kitten-hints-multiple).
    Default: `auto`
    Choices: `always`, `auto`, `never`

--hints-offset <HINTS\_OFFSET>[¶](#cmdoption-kitty-kitten-hints-hints-offset "Link to this definition")
:   The offset (from zero) at which to start hint numbering. Note that only numbers greater than or equal to zero are respected.
    Default: `1`

--alphabet <ALPHABET>[¶](#cmdoption-kitty-kitten-hints-alphabet "Link to this definition")
:   The list of characters to use for hints. The default is to use numbers and lowercase English alphabets. Specify your preference as a string of characters. Note that you need to specify the [`--hints-offset`](#cmdoption-kitty-kitten-hints-hints-offset) as zero to use the first character to highlight the first match, otherwise it will start with the second character by default.

--ascending [=no][¶](#cmdoption-kitty-kitten-hints-ascending "Link to this definition")
:   Make the hints increase from top to bottom, instead of decreasing from top to bottom.

--hints-foreground-color <HINTS\_FOREGROUND\_COLOR>[¶](#cmdoption-kitty-kitten-hints-hints-foreground-color "Link to this definition")
:   The foreground color for hints. You can use color names or hex values. For the eight basic named terminal colors you can also use the `bright-` prefix to get the bright variant of the color.
    Default: `black`

--hints-background-color <HINTS\_BACKGROUND\_COLOR>[¶](#cmdoption-kitty-kitten-hints-hints-background-color "Link to this definition")
:   The background color for hints. You can use color names or hex values. For the eight basic named terminal colors you can also use the `bright-` prefix to get the bright variant of the color.
    Default: `green`

--hints-text-color <HINTS\_TEXT\_COLOR>[¶](#cmdoption-kitty-kitten-hints-hints-text-color "Link to this definition")
:   The foreground color for text pointed to by the hints. You can use color names or hex values. For the eight basic named terminal colors you can also use the `bright-` prefix to get the bright variant of the color. The default is to pick a suitable color automatically.
    Default: `auto`

--customize-processing <CUSTOMIZE\_PROCESSING>[¶](#cmdoption-kitty-kitten-hints-customize-processing "Link to this definition")
:   Name of a python file in the kitty config directory which will be imported to provide custom implementations for pattern finding and performing actions on selected matches. You can also specify absolute paths to load the script from elsewhere. See <https://sw.kovidgoyal.net/kitty/kittens/hints/> for details.

--window-title <WINDOW\_TITLE>[¶](#cmdoption-kitty-kitten-hints-window-title "Link to this definition")
:   The title for the hints window, default title is based on the type of text being hinted.

Note

To avoid having to specify the same command line options on every
invocation, you can use the [`action_alias`](../../conf/#opt-kitty.action_alias) option in
`kitty.conf`, creating aliases that have common sets of options.
For example:

```
action_alias myhints kitten hints --alphabet qfjdkslaureitywovmcxzpq1234567890
map f1 myhints --customize-processing custom-hints.py
```
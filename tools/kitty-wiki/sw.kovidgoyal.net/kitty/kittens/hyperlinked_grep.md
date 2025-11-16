---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/hyperlinked_grep/"
title: "Hyperlinked grep - kitty"
crawl_date: "2025-11-16T14:48:34.882082Z"
selector: "article"
---

# Hyperlinked grep - kitty

# Hyperlinked grep[¶](#hyperlinked-grep "Link to this heading")

Note

As of ripgrep versions newer that 13.0 it supports hyperlinks
natively so you can just add the following alias in your shell rc file:
`alias rg="rg --hyperlink-format=kitty"` no need to use this kitten.
But, see below for instructions on how to customize kitty to have it open
the hyperlinks from ripgrep in your favorite editor.

This kitten allows you to search your files using [ripgrep](https://github.com/BurntSushi/ripgrep) and open the results directly in your
favorite editor in the terminal, at the line containing the search result,
simply by clicking on the result you want.

Added in version 0.19.0.

To set it up, first create `~/.config/kitty/open-actions.conf` with the
following contents:

```
# Open any file with a fragment in vim, fragments are generated
# by the hyperlink-grep kitten and nothing else so far.
protocol file
fragment_matches [0-9]+
action launch --type=overlay --cwd=current vim +${FRAGMENT} -- ${FILE_PATH}

# Open text files without fragments in the editor
protocol file
mime text/*
action launch --type=overlay --cwd=current -- ${EDITOR} -- ${FILE_PATH}
```

Now, run a search with:

```
kitten hyperlinked-grep something
```

Hold down the `Ctrl`+`Shift` keys and click on any of the result lines, to
open the file in **vim** at the matching line. If you use some editor
other than **vim**, you should adjust the `open-actions.conf` file
accordingly. TO open links with the keyboard instead, use
[`ctrl+shift+p>y`](../../conf/#shortcut-kitty.Open-the-selected-hyperlink).

Finally, add an alias to your shell’s rc files to invoke the kitten as
**hg**:

```
alias hg="kitten hyperlinked-grep"
```

You can now run searches with:

```
hg some-search-term
```

To learn more about kitty’s powerful framework for customizing URL click
actions, see [here](../../open_actions/).

By default, this kitten adds hyperlinks for several parts of ripgrep output:
the per-file header, match context lines, and match lines. You can control
which items are linked with a `--kitten hyperlink` flag. For example,
`--kitten hyperlink=matching_lines` will only add hyperlinks to the
match lines. `--kitten hyperlink=file_headers,context_lines` will link
file headers and context lines but not match lines. `--kitten
hyperlink=none` will cause the command line to be passed to directly to
**rg** so no hyperlinking will be performed. `--kitten hyperlink`
may be specified multiple times.

Hopefully, someday this functionality will make it into some [upstream grep](https://github.com/BurntSushi/ripgrep/issues/665) program directly removing
the need for this kitten.

Note

While you can pass any of ripgrep’s command line options to the kitten and
they will be forwarded to **rg**, do not use options that change the
output formatting as the kitten works by parsing the output from ripgrep.
The unsupported options are: `--context-separator`,
`--field-context-separator`, `--field-match-separator`,
`--json`, `-I --no-filename`, `-0 --null`,
`--null-data`, `--path-separator`. If you specify options via
configuration file, then any changes to the default output format will not be
supported, not just the ones listed.
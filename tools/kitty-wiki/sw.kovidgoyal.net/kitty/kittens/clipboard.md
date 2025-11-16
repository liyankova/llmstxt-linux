---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/clipboard/"
title: "clipboard - kitty"
crawl_date: "2025-11-16T14:48:49.621893Z"
selector: "article"
---

# clipboard - kitty

# clipboard[¶](#clipboard "Link to this heading")

*Copy/paste to the system clipboard from shell scripts*

The `clipboard` kitten can be used to read or write to the system clipboard
from the shell. It even works over SSH. Using it is as simple as:

```
echo hooray | kitten clipboard
```

All text received on `STDIN` is copied to the clipboard.

To get text from the clipboard:

```
kitten clipboard --get-clipboard
```

The text will be written to `STDOUT`. Note that by default kitty asks for
permission when a program attempts to read the clipboard. This can be
controlled via [`clipboard_control`](../../conf/#opt-kitty.clipboard_control).

Added in version 0.27.0: Support for copying arbitrary data types

The clipboard kitten can be used to send/receive
more than just plain text from the system clipboard. You can transfer arbitrary
data types. Best illustrated with some examples:

```
# Copy an image to the clipboard:
kitten clipboard picture.png

# Copy an image and some text to the clipboard:
kitten clipboard picture.jpg text.txt

# Copy text from STDIN and an image to the clipboard:
echo hello | kitten clipboard picture.png /dev/stdin

# Copy any raster image available on the clipboard to a PNG file:
kitten clipboard -g picture.png

# Copy an image to a file and text to STDOUT:
kitten clipboard -g picture.png /dev/stdout

# List the formats available on the system clipboard
kitten clipboard -g -m . /dev/stdout
```

Normally, the kitten guesses MIME types based on the file names. To control the
MIME types precisely, use the [`--mime`](#cmdoption-kitty-kitten-clipboard-mime) option.

This kitten uses a new protocol developed by kitty to function, for details,
see [Copying all data types to the clipboard](../../clipboard/).

## Source code for clipboard[¶](#source-code-for-clipboard "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/clipboard).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten clipboard [options] [files to copy to/from]
```

Read or write to the system clipboard.

This kitten operates most simply in filter mode.
To set the clipboard text, pipe in the new text on `STDIN`. Use the
[`--get-clipboard`](#cmdoption-kitty-kitten-clipboard-get-clipboard) option to instead output the current clipboard text content to
`STDOUT`. Note that copying from the clipboard will cause a permission
popup, see [`clipboard_control`](../../conf/#opt-kitty.clipboard_control) for details.

For more control, specify filename arguments. Then, different MIME types can be copied to/from
the clipboard. Some examples:

```
# Copy an image to the clipboard:
kitten clipboard picture.png

# Copy an image and some text to the clipboard:
kitten clipboard picture.jpg text.txt

# Copy text from STDIN and an image to the clipboard:
echo hello | kitten clipboard picture.png /dev/stdin

# Copy any raster image available on the clipboard to a PNG file:
kitten clipboard -g picture.png

# Copy an image to a file and text to STDOUT:
kitten clipboard -g picture.png /dev/stdout

# List the formats available on the system clipboard
kitten clipboard -g -m . /dev/stdout
```

### Options[¶](#options "Link to this heading")

--get-clipboard [=no], -g [=no][¶](#cmdoption-kitty-kitten-clipboard-get-clipboard "Link to this definition")
:   Output the current contents of the clipboard to STDOUT. Note that by default kitty will prompt for permission to access the clipboard. Can be controlled by [`clipboard_control`](../../conf/#opt-kitty.clipboard_control).

--use-primary [=no], -p [=no][¶](#cmdoption-kitty-kitten-clipboard-use-primary "Link to this definition")
:   Use the primary selection rather than the clipboard on systems that support it, such as Linux.

--mime <MIME>, -m <MIME>[¶](#cmdoption-kitty-kitten-clipboard-mime "Link to this definition")
:   The mimetype of the specified file. Useful when the auto-detected mimetype is likely to be incorrect or the filename has no extension and therefore no mimetype can be detected. If more than one file is specified, this option should be specified multiple times, once for each specified file. When copying data from the clipboard, you can use wildcards to match MIME types. For example: `--mime 'text/*'` will match any textual MIME type available on the clipboard, usually the first matching MIME type is copied. The special MIME type `.` will return the list of available MIME types currently on the system clipboard.

--alias <ALIAS>, -a <ALIAS>[¶](#cmdoption-kitty-kitten-clipboard-alias "Link to this definition")
:   Specify aliases for MIME types. Aliased MIME types are considered equivalent. When copying to clipboard both the original and alias are made available on the clipboard. When copying from clipboard if the original is not found, the alias is used, as a fallback. Can be specified multiple times to create multiple aliases. For example: `--alias text/plain=text/x-rst` makes `text/plain` an alias of `text/rst`. Aliases are not used in filter mode. An alias for `text/plain` is automatically created if `text/plain` is not present in the input data, but some other `text/*` MIME is present.

--wait-for-completion [=no][¶](#cmdoption-kitty-kitten-clipboard-wait-for-completion "Link to this definition")
:   Wait till the copy to clipboard is complete before exiting. Useful if running the kitten in a dedicated, ephemeral window. Only needed in filter mode.

--password <PASSWORD>[¶](#cmdoption-kitty-kitten-clipboard-password "Link to this definition")
:   A password to use when accessing the clipboard. If the user chooses to accept the password future invocations of the kitten will not have a permission prompt in this tty session. Does not work in filter mode. Must be of the form: text:actual-password or fd:integer (a file descriptor number to read the password from) or file:path-to-file (a file from which to read the password). Note that you must also specify a human friendly name using the [`--human-name`](#cmdoption-kitty-kitten-clipboard-human-name) flag.

--human-name <HUMAN\_NAME>[¶](#cmdoption-kitty-kitten-clipboard-human-name "Link to this definition")
:   A human friendly name to show the user when asking for permission to access the clipboard.
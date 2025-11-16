---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/query_terminal/"
title: "Query terminal - kitty"
crawl_date: "2025-11-16T14:48:58.730866Z"
selector: "article"
---

# Query terminal - kitty

# Query terminal[¶](#query-terminal "Link to this heading")

This kitten is used to query *kitty* from terminal programs about version, values
of various runtime options controlling its features, etc.

The querying is done using the (*semi*) standard XTGETTCAP escape sequence
pioneered by xterm, so it works over SSH as well. The downside is that it is
slow, since it requires a roundtrip to the terminal emulator and back.

If you want to do some of the same querying in your terminal program without
depending on the kitten, you can do so, by processing the same escape codes.
Search [this page](https://invisible-island.net/xterm/ctlseqs/ctlseqs.html)
for *XTGETTCAP* to see the syntax for the escape code. The kitty specific keys
are all documented below, when sent via escape code they must be prefixed with
`kitty-query-`.

## Source code for query\_terminal[¶](#source-code-for-query-terminal "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/query_terminal).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten query_terminal [options] [query1 query2 ...]
```

Query the terminal this kitten is run in for various capabilities. This sends
escape codes to the terminal and based on its response prints out data about
supported capabilities. Note that this is a blocking operation, since it has to
wait for a response from the terminal. You can control the maximum wait time via
the `--wait-for` option.

The output is lines of the form:

```
query: data
```

If a particular query is unsupported by the running kitty version, the
data will be blank.

Note that when calling this from another program, be very careful not to perform
any I/O on the terminal device until this kitten exits.

Available queries are:

`name`:
:   Terminal name (e.g. `xterm-kitty`)

`version`:
:   Terminal version (e.g. `0.44.0`)

`allow_hyperlinks`:
:   The config option [`allow_hyperlinks`](../../conf/#opt-kitty.allow_hyperlinks) in `kitty.conf` for allowing hyperlinks can be `yes`, `no` or `ask`

`font_family`:
:   The current font’s PostScript name

`bold_font`:
:   The current bold font’s PostScript name

`italic_font`:
:   The current italic font’s PostScript name

`bold_italic_font`:
:   The current bold-italic font’s PostScript name

`font_size`:
:   The current font size in pts

`dpi_x`:
:   The current DPI on the x-axis

`dpi_y`:
:   The current DPI on the y-axis

`foreground`:
:   The current foreground color as a 24-bit # color code

`background`:
:   The current background color as a 24-bit # color code

`background_opacity`:
:   The current background opacity as a number between 0 and 1

`clipboard_control`:
:   The config option [`clipboard_control`](../../conf/#opt-kitty.clipboard_control) in `kitty.conf` for allowing reads/writes to/from the clipboard

`os_name`:
:   The name of the OS the terminal is running on. kitty returns values: bsd, linux, macos, unknown

### Options[¶](#options "Link to this heading")

--wait-for <WAIT\_FOR>[¶](#cmdoption-kitty-kitten-query_terminal-wait-for "Link to this definition")
:   The amount of time (in seconds) to wait for a response from the terminal, after querying it.
    Default: `10`
---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/unicode_input/"
title: "Unicode input - kitty"
crawl_date: "2025-11-16T14:48:19.462202Z"
selector: "article"
---

# Unicode input - kitty

# Unicode input[¶](#unicode-input "Link to this heading")

You can input Unicode characters by name, hex code, recently used and even an
editable favorites list. Press [`ctrl+shift+u`](../../conf/#shortcut-kitty.Unicode-input) to start the
unicode input kitten, shown below.

[![A screenshot of the unicode input kitten](../../_images/unicode.png)](../../_images/unicode.png)

A screenshot of the unicode input kitten[¶](#id1 "Link to this image")

In Code mode, you enter a Unicode character by typing in the hex
code for the character and pressing `Enter`. For example, type in `2716`
and press `Enter` to get `✖`. You can also choose a character from the
list of recently used characters by typing a leading period `.` and then the
two character index and pressing `Enter`.
The `Up` and `Down` arrow keys can be used to choose the previous and
next Unicode symbol respectively.

In Name mode you instead type words from the character name and use
the `ArrowKeys` / `Tab` to select the character from the displayed
matches. You can also type a space followed by a period and the index for the
match if you don’t like to use arrow keys.

You can switch between modes using either the keys `F1` … `F4` or
`Ctrl`+`1` … `Ctrl`+`4` or by pressing `Ctrl`+`[` and `Ctrl`+`]`
or by pressing `Ctrl`+`Tab` and `Ctrl`+`Shift`+`Tab`.

## Source code for unicode\_input[¶](#source-code-for-unicode-input "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/unicode_input).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten unicode_input [options]
```

Input a Unicode character

### Options[¶](#options "Link to this heading")

--emoji-variation <EMOJI\_VARIATION>[¶](#cmdoption-kitty-kitten-unicode_input-emoji-variation "Link to this definition")
:   Whether to use the textual or the graphical form for emoji. By default the default form specified in the Unicode standard for the symbol is used.
    Default: `none`
    Choices: `graphic`, `none`, `text`

--tab <TAB>[¶](#cmdoption-kitty-kitten-unicode_input-tab "Link to this definition")
:   The initial tab to display. Defaults to using the tab from the previous kitten invocation.
    Default: `previous`
    Choices: `code`, `emoticons`, `favorites`, `name`, `previous`
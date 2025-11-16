---
source_url: "https://sw.kovidgoyal.net/kitty/marks/"
title: "Mark text on screen - kitty"
crawl_date: "2025-11-16T14:49:36.652470Z"
selector: "article"
---

# Mark text on screen - kitty

# Mark text on screen[¶](#mark-text-on-screen "Link to this heading")

kitty has the ability to mark text on the screen based on regular expressions.
This can be useful to highlight words or phrases when browsing output from long
running programs or similar. Lets start with a few examples:

# Examples[¶](#examples "Link to this heading")

Suppose we want to be able to highlight the word `ERROR` in the current
window. Add the following to `kitty.conf`:

```
map f1 toggle_marker text 1 ERROR
```

Now when you press `F1`, all instances of the word `ERROR` will be
highlighted. To turn off the highlighting, press `F1` again.
If you want to make it case-insensitive, use:

```
map f1 toggle_marker itext 1 ERROR
```

To make it match only complete words, use:

```
map f1 toggle_marker regex 1 \\bERROR\\b
```

Suppose you want to highlight both `ERROR` and `WARNING`, case
insensitively:

```
map f1 toggle_marker iregex 1 \\bERROR\\b 2 \\bWARNING\\b
```

kitty supports up to 3 mark groups (the numbers in the commands above). You
can control the colors used for these groups in `kitty.conf` with:

```
mark1_foreground red
mark1_background gray
mark2_foreground green
...
```

Note

For performance reasons, matching is done per line only, and only when that
line is altered in any way. So you cannot match text that stretches across
multiple lines.

# Creating markers dynamically[¶](#creating-markers-dynamically "Link to this heading")

If you want to create markers dynamically rather than pre-defining them in
`kitty.conf`, you can do so as follows:

```
map f1 create_marker
map f2 remove_marker
```

Then pressing `F1` will allow you to enter the marker definition and set it
and pressing `F2` will remove the marker. [`create_marker`](../actions/#action-create_marker) accepts the
same syntax as [`toggle_marker`](../actions/#action-toggle_marker) above. Note that while creating markers, the
prompt has history so you can easily re-use previous marker expressions.

You can also use the facilities for [Control kitty from scripts](../remote-control/) to dynamically add or
remove markers.

# Scrolling to marks[¶](#scrolling-to-marks "Link to this heading")

kitty has a [`scroll_to_mark`](../actions/#action-scroll_to_mark) action to scroll to the next line that contains
a mark. You can use it by mapping it to some shortcut in `kitty.conf`:

```
map ctrl+p scroll_to_mark prev
map ctrl+n scroll_to_mark next
```

Then pressing `Ctrl`+`P` will scroll to the first line in the scrollback
buffer above the current top line that contains a mark. Pressing `Ctrl`+`N`
will scroll to show the first line below the current last line that contains
a mark. If you wish to jump to a mark of a specific type, you can add that to
the mapping:

```
map ctrl+1 scroll_to_mark prev 1
```

Which will scroll only to marks of type 1.

# The full syntax for creating marks[¶](#the-full-syntax-for-creating-marks "Link to this heading")

The syntax of the [`toggle_marker`](../actions/#action-toggle_marker) action is:

```
toggle_marker <marker-type> <specification>
```

Here `marker-type` is one of:

* `text` - Simple substring matching
* `itext` - Case-insensitive substring matching
* `regex` - A Python regular expression
* `iregex` - A case-insensitive Python regular expression
* `function` - An arbitrary function defined in a Python file, see [Arbitrary marker functions](#marker-funcs).

# Arbitrary marker functions[¶](#arbitrary-marker-functions "Link to this heading")

You can create your own marker functions. Create a Python file named
`mymarker.py` and in it create a `marker` function. This function
receives the text of the line as input and must yield three numbers,
the starting character position, the ending character position and the mark
group (1-3). For example:

```
def marker(text):
    # Function to highlight the letter X
    for i, ch in enumerate(text):
        if ch.lower() == 'x':
            yield i, i, 3
```

Save this file somewhere and in `kitty.conf`, use:

```
map f1 toggle_marker function /path/to/mymarker.py
```

If you save the file in the [kitty config directory](../conf/#confloc), you can
use:

```
map f1 toggle_marker function mymarker.py
```
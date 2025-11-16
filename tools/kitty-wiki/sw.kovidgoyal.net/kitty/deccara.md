---
source_url: "https://sw.kovidgoyal.net/kitty/deccara/"
title: "Setting text styles/colors in arbitrary regions of the screen - kitty"
crawl_date: "2025-11-16T14:50:49.043771Z"
selector: "article"
---

# Setting text styles/colors in arbitrary regions of the screen - kitty

# Setting text styles/colors in arbitrary regions of the screen[¶](#setting-text-styles-colors-in-arbitrary-regions-of-the-screen "Link to this heading")

There already exists an escape code to set *some* text attributes in arbitrary
regions of the screen, [DECCARA](https://vt100.net/docs/vt510-rm/DECCARA.html). However, it is limited to
only a few attributes. *kitty* extends this to work with *all* SGR attributes.
So, for example, this can be used to set the background color in an arbitrary
region of the screen.

The motivation for this extension is the various problems with the existing
solution for erasing to background color, namely the *background color erase
(bce)* capability. See [this discussion](https://github.com/kovidgoyal/kitty/issues/160#issuecomment-346470545)
and [this FAQ](https://invisible-island.net/ncurses/ncurses.faq.html#bce_mismatches)
for a summary of problems with *bce*.

For example, to set the background color to blue in a rectangular region of the
screen from (3, 4) to (10, 11), you use:

```
<ESC>[2*x<ESC>[4;3;11;10;44$r<ESC>[*x
```
---
source_url: "https://sw.kovidgoyal.net/kitty/protocol-extensions/"
title: "Terminal protocol extensions - kitty"
crawl_date: "2025-11-16T14:50:04.101520Z"
selector: "article"
---

# Terminal protocol extensions - kitty

# Terminal protocol extensions[¶](#terminal-protocol-extensions "Link to this heading")

*kitty* has extensions to the legacy terminal protocol, to enable advanced
features. These are typically in the form of new or re-purposed escape codes.
While these extensions are currently *kitty* specific, it would be nice to get
some of them adopted more broadly, to push the state of terminal emulators
forward.

The goal of these extensions is to be as small and unobtrusive as possible,
while filling in some gaps in the existing xterm protocol. In particular, one of
the goals of this specification is explicitly not to “re-imagine” the TTY. The
TTY should remain what it is -- a device for efficiently processing text
received as a simple byte stream. Another objective is to only move the minimum
possible amount of extra functionality into the terminal program itself. This is
to make it as easy to implement these protocol extensions as possible, thereby
hopefully encouraging their widespread adoption.

If you wish to discuss these extensions, propose additions or changes to them,
please do so by opening issues in the [GitHub bug tracker](https://github.com/kovidgoyal/kitty/issues).

* [Colored and styled underlines](../underlines/)
* [Terminal graphics protocol](../graphics-protocol/)
* [Comprehensive keyboard handling in terminals](../keyboard-protocol/)
* [The text sizing protocol](../text-sizing-protocol/)
* [The multiple cursors protocol](../multiple-cursors-protocol/)
* [File transfer over the TTY](../file-transfer-protocol/)
* [Desktop notifications](../desktop-notifications/)
* [Mouse pointer shapes](../pointer-shapes/)
* [Unscrolling the screen](../unscroll/)
* [Color control](../color-stack/)
* [Setting text styles/colors in arbitrary regions of the screen](../deccara/)
* [Copying all data types to the clipboard](../clipboard/)
* [Miscellaneous protocol extensions](../misc-protocol/)
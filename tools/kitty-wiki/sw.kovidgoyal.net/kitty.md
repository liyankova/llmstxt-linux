---
source_url: "https://sw.kovidgoyal.net/kitty/"
title: "kitty"
crawl_date: "2025-11-16T14:47:48.379575Z"
selector: "article"
---

# kitty

# kitty[¶](#kitty "Link to this heading")

*If you live in the terminal, kitty is made for YOU!*

The fast, feature-rich, GPU based terminal emulator.

Fast

* Uses GPU and SIMD vector CPU instructions for [best in class performance](performance/)
* Uses threaded rendering for [absolutely minimal latency](https://github.com/kovidgoyal/kitty/issues/2701#issuecomment-636497270)
* Performance tradeoffs can be [tuned](conf/#conf-kitty-performance)

Capable

* Graphics, with [images and animations](graphics-protocol/)
* Ligatures, emoji with [`per glyph font substitution`](conf/#opt-kitty.symbol_map) and [variable fonts and font features](kittens/choose-fonts/)
* [Hyperlinks](glossary/#term-hyperlinks), with [configurable actions](open_actions/)

Scriptable

* Control from [scripts or the shell](remote-control/)
* Extend with [kittens](kittens_intro/#kittens) using the Python language
* Use [startup sessions](sessions/#sessions) to specify working environments

Composable

* Programmable tabs, [splits](layouts/#splits-layout) and multiple [layouts](layouts/) to manage windows
* Browse the [entire history](overview/#scrollback) or the [`output from the last command`](conf/#shortcut-kitty.Browse-output-of-the-last-shell-command-in-pager)
  comfortably in pagers and editors
* Edit or download [remote files](kittens/remote_file/) in an existing SSH session

Cross-platform

* Linux
* macOS
* Various BSDs

Innovative

Pioneered various extensions to move the entire terminal ecosystem forward

* [Terminal graphics protocol](graphics-protocol/)
* [Comprehensive keyboard handling in terminals](keyboard-protocol/)
* Lots more in [Terminal protocol extensions](protocol-extensions/)

To get started see [Quickstart](quickstart/).

[![

](_static/poster.png)](https://download.calibre-ebook.com/videos/kitty.mp4)

Watch kitty in action!

Timestamps for the above video:

00:00
:   Intro

00:39
:   Pager: View command output in same window: `Ctrl`+`Shift`+`g`

01:43
:   Pager: View command output in a separate window

02:14
:   Pager: Uses shell integration in kitty

02:27
:   Tab text: The output of cwd and last cmd

03:03
:   Open files from ls output with mouse: `Ctrl`+`Shift`+`Right`-`click`

04:04
:   Open files from ls output with keyboard: `Ctrl`+`Shift`+`P>y`

04:26
:   Open files on click: `ls --hyperlink=auto`

05:03
:   Open files on click: Filetype settings in open-actions.conf

05:45
:   hyperlinked-grep kitten: Open grep output in editor

07:18
:   Remote-file kitten: View remote files locally

08:31
:   Remote-file kitten: Edit remote files locally

10:01
:   icat kitten: View images directly

10:36
:   icat kitten: Download & display image/gif from internet

11:03
:   Kitty Graphics Protocol: Live image preview in ranger

11:25
:   icat kitten: Display image from remote server

12:04
:   unicode-input kitten: Emojis in terminal

12:54
:   Windows: Intro

13:36
:   Windows: Switch focus: `Ctrl`+`Shift`+`win_nr`

13:48
:   Windows: Visual selection: `Ctrl`+`Shift`+`F7`

13:58
:   Windows: Simultaneous input

14:15
:   Interactive Kitty Shell: `Ctrl`+`Shift`+`Esc`

14:36
:   Broadcast text: `launch --allow-remote-control kitten broadcast`

15:18
:   Kitty Remote Control Protocol

15:52
:   Interactive Kitty Shell: Help

16:34
:   Choose theme interactively: `kitten themes -h`

17:23
:   Choose theme by name: `kitten themes [options] [theme_name]`
---
source_url: "https://sw.kovidgoyal.net/kitty/integrations/"
title: "Integrations with other tools - kitty"
crawl_date: "2025-11-16T14:50:01.403708Z"
selector: "article"
---

# Integrations with other tools - kitty

# Integrations with other tools[¶](#integrations-with-other-tools "Link to this heading")

kitty provides extremely powerful interfaces such as [Control kitty from scripts](../remote-control/) and
[Custom kittens](../kittens/custom/) and [icat](../kittens/icat/) that allow it to be integrated
with other tools seamlessly.

## Image and document viewers[¶](#image-and-document-viewers "Link to this heading")

Powered by kitty’s [Terminal graphics protocol](../graphics-protocol/) there exist many tools for viewing
images and other types of documents directly in your terminal, even over SSH.

### [termpdf.py](https://github.com/dsanson/termpdf.py)[¶](#tool-termpdf "Link to this heading")

A terminal PDF/DJVU/CBR viewer

### [tdf](https://github.com/itsjunetime/tdf)[¶](#tool-tdf "Link to this heading")

A terminal PDF viewer

### [fancy-cat](https://github.com/freref/fancy-cat)[¶](#tool-fancy-cat "Link to this heading")

A terminal PDF viewer

### [meowpdf](https://github.com/monoamine11231/meowpdf)[¶](#tool-meowpdf "Link to this heading")

A terminal PDF viewer with GUI-like usage and Vim-like keybindings written in Rust

### [mcat](https://github.com/Skardyy/mcat)[¶](#tool-mcat "Link to this heading")

Display various types of files nicely formatted with images in the terminal

### [ranger](https://github.com/ranger/ranger)[¶](#tool-ranger "Link to this heading")

A terminal file manager, with previews of file contents powered by kitty’s
graphics protocol.

### [nnn](https://github.com/jarun/nnn/)[¶](#tool-nnn "Link to this heading")

Another terminal file manager, with previews of file contents powered by kitty’s
graphics protocol.

### [Yazi](https://github.com/sxyazi/yazi)[¶](#tool-yazi "Link to this heading")

Blazing fast terminal file manager, with built-in kitty graphics protocol support
(implemented both Classic protocol and Unicode placeholders).

### [clifm](https://github.com/leo-arch/clifm)[¶](#clifm "Link to this heading")

The shell-like, command line terminal file manager, uses the kitty graphics and
keyboard protocols.

### [hunter](https://github.com/rabite0/hunter)[¶](#tool-hunter "Link to this heading")

Another terminal file manager, with previews of file contents powered by kitty’s
graphics protocol.

### [presenterm](https://github.com/mfontanini/presenterm)[¶](#tool-presentterm "Link to this heading")

Show markdown based slides with images in your terminal, powered by the
kitty graphics protocol.

### [term-image](https://github.com/AnonymouX47/term-image)[¶](#term-image "Link to this heading")

Tool to browse images in a terminal using kitty’s graphics protocol.

### [koneko](https://github.com/twenty5151/koneko)[¶](#tool-koneko "Link to this heading")

Browse images from the pixiv artist community directly in kitty.

### [viu](https://github.com/atanunq/viu)[¶](#tool-viu "Link to this heading")

View images in the terminal, similar to kitty’s icat.

### [nb](https://github.com/xwmx/nb)[¶](#tool-nb "Link to this heading")

Command line and local web note-taking, bookmarking, archiving, and knowledge
base application that uses kitty’s graphics protocol for images.

### [w3m](https://github.com/tats/w3m)[¶](#tool-w3m "Link to this heading")

A text mode WWW browser that supports kitty’s graphics protocol to display
images.

### [awrit](https://github.com/chase/awrit)[¶](#awrit "Link to this heading")

A full Chromium based web browser running in the terminal using kitty’s
graphics protocol.

### [chawan](https://sr.ht/~bptato/chawan/)[¶](#chawan "Link to this heading")

A text mode WWW browser that supports kitty’s graphics protocol to display
images.

### [mpv](https://github.com/mpv-player/mpv/commit/874e28f4a41a916bb567a882063dd2589e9234e1)[¶](#tool-mpv "Link to this heading")

A video player that can play videos in the terminal.

```
mpv --profile=sw-fast --vo=kitty --vo-kitty-use-shm=yes --really-quiet video.mkv
```

### [timg](https://github.com/hzeller/timg)[¶](#tool-timg "Link to this heading")

A terminal image and video viewer, that displays static and animated images or
plays videos. Fast multi-threaded loading, JPEG exif rotation, grid view and
connecting to the webcam make it a versatile terminal utility.

## System and data visualisation tools[¶](#system-and-data-visualisation-tools "Link to this heading")

### [neofetch](https://github.com/dylanaraps/neofetch)[¶](#tool-neofetch "Link to this heading")

A command line system information tool that shows images using kitty’s graphics
protocol

### matplotlib[¶](#matplotlib "Link to this heading")

There exist multiple backends for matplotlib to draw images directly in kitty.

* [matplotlib-backend-kitty](https://github.com/jktr/matplotlib-backend-kitty)
* [kitcat](https://github.com/mil-ad/kitcat)

### [KittyTerminalImages.jl](https://github.com/simonschoelly/KittyTerminalImages.jl)[¶](#tool-kittyterminalimage "Link to this heading")

Show images from Julia directly in kitty

### [euporie](https://github.com/joouha/euporie)[¶](#tool-euporie "Link to this heading")

A text-based user interface for running and editing Jupyter notebooks, powered
by kitty’s graphics protocol for displaying plots

### [gnuplot](http://www.gnuplot.info/)[¶](#tool-gnuplot "Link to this heading")

A graphing and data visualization tool that can be made to display its output in
kitty with the following bash snippet:

```
function iplot {
    cat <<EOF | gnuplot
    set terminal pngcairo enhanced font 'Fira Sans,10'
    set autoscale
    set samples 1000
    set output '|kitten icat --stdin yes'
    set object 1 rectangle from screen 0,0 to screen 1,1 fillcolor rgb"#fdf6e3" behind
    plot $@
    set output '/dev/null'
EOF
}
```

Add this to bashrc and then to plot a function, simply do:

```
iplot 'sin(x*3)*exp(x*.2)'
```

### [k-nine](https://github.com/talwrii/kitty-plotnine)[¶](#tool-k-nine "Link to this heading")

A wrapper around the `plotnine` library which lets you plot data from the command-line with bash one-liners.

### [tgutui](https://github.com/tgu-ltd/tgutui)[¶](#id22 "Link to this heading")

A Terminal Operating Test hardware equipment

### [onefetch](https://github.com/o2sh/onefetch)[¶](#id23 "Link to this heading")

A tool to fetch information about your git repositories

### [patat](https://github.com/jaspervdj/patat)[¶](#id24 "Link to this heading")

Terminal based presentations using pandoc and kitty’s image protocol for
images

### [wttr.in](https://github.com/chubin/wttr.in)[¶](#id25 "Link to this heading")

A tool to display weather information in your terminal with curl

### [wl-clipboard-manager](https://github.com/maximbaz/wl-clipboard-manager)[¶](#id26 "Link to this heading")

View and manage the system clipboard under Wayland in your kitty terminal

### [NEMU](https://github.com/nemuTUI/nemu)[¶](#nemu "Link to this heading")

TUI for QEMU used to manage virtual machines, can display the Virtual Machine
in the terminal using the kitty graphics protocol.

## Editor integration[¶](#editor-integration "Link to this heading")

*kitty* can be integrated into many different terminal based text editors to add
features such a split windows, previews, REPLs etc.

### [kakoune](https://kakoune.org/)[¶](#id27 "Link to this heading")

Integrates with kitty to use native kitty windows for its windows/panels and
REPLs.

### [vim-slime](https://github.com/jpalardy/vim-slime#kitty)[¶](#id28 "Link to this heading")

Uses kitty remote control for a Lisp REPL.

### [vim-kitty-navigator](https://github.com/knubie/vim-kitty-navigator)[¶](#id29 "Link to this heading")

Allows you to navigate seamlessly between vim and kitty splits using a
consistent set of hotkeys.

### [vim-test](https://github.com/vim-test/vim-test)[¶](#id30 "Link to this heading")

Allows easily running tests in a terminal window

### Various image viewing plugins for editors[¶](#various-image-viewing-plugins-for-editors "Link to this heading")

* [snacks.nvim](https://github.com/folke/snacks.nvim) - Enables seamless inline images in various file formats within nvim
* [image.nvim](https://github.com/3rd/image.nvim) - Bringing images to neovim
* [image\_preview.nvim](https://github.com/adelarsq/image_preview.nvim/) - Image preview for neovim
* [hologram.nvim](https://github.com/edluffy/hologram.nvim) - view images inside nvim

## Scrollback manipulation[¶](#scrollback-manipulation "Link to this heading")

### [kitty-scrollback.nvim](https://github.com/mikesmithgh/kitty-scrollback.nvim)[¶](#id31 "Link to this heading")

Browse the scrollback buffer with Neovim, with simple key actions for efficient
copy/paste and even execution of commands.

### [kitty-search](https://github.com/trygveaa/kitty-kitten-search)[¶](#id32 "Link to this heading")

Live incremental search of the scrollback buffer.

### [kitty-grab](https://github.com/yurikhan/kitty_grab)[¶](#id33 "Link to this heading")

Keyboard based text selection for the kitty scrollback buffer.

## Desktop panels[¶](#desktop-panels "Link to this heading")

### [kitty panel](https://github.com/5hubham5ingh/kitty-panel)[¶](#kitty-panel "Link to this heading")

A system panel for Kitty terminal that displays real-time system metrics using terminal-based utilities.

### [pawbar](https://github.com/codelif/pawbar)[¶](#pawbar "Link to this heading")

A kitten-panel based desktop panel for your desktop

## Password managers[¶](#password-managers "Link to this heading")

### [1password](https://github.com/mm-zacharydavison/kitty-kitten-1password)[¶](#password "Link to this heading")

Allow injecting passwords from 1Password into kitty.

### [BitWarden](https://github.com/dnanhkhoa/kitty-password-manager)[¶](#bitwarden "Link to this heading")

Inject passwords from ButWarden into kitty

## Miscellaneous[¶](#miscellaneous "Link to this heading")

### DOOM[¶](#doom "Link to this heading")

Play the classic shooter DOOM in [kitty](https://github.com/cryptocode/terminal-doom) or even inside [neovim inside kitty](https://github.com/seandewar/actually-doom.nvim).

### [gattino](https://github.com/salvozappa/gattino)[¶](#gattino "Link to this heading")

Integrate kitty with an LLM to convert plain language prompts into shell
commands.

### [kitty-smart-tab](https://github.com/yurikhan/kitty-smart-tab)[¶](#id34 "Link to this heading")

Use keys to either control tabs or pass them onto running applications if no
tabs are present

### [kitty-smart-scroll](https://github.com/yurikhan/kitty-smart-scroll)[¶](#id35 "Link to this heading")

Use keys to either scroll or pass them onto running applications if no
scrollback buffer is present

### [kitti3](https://github.com/LandingEllipse/kitti3)[¶](#id36 "Link to this heading")

Allow using kitty as a drop-down terminal under the i3 window manager

### [weechat-hints](https://github.com/GermainZ/kitty-weechat-hints)[¶](#id37 "Link to this heading")

URL hints kitten for WeeChat that works without having to use WeeChat’s
raw-mode.

### [glkitty](https://github.com/michaeljclark/glkitty)[¶](#id38 "Link to this heading")

C library to draw OpenGL shaders in the terminal with a glgears demo
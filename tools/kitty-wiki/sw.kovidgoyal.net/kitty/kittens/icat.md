---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/icat/"
title: "icat - kitty"
crawl_date: "2025-11-16T14:48:16.198165Z"
selector: "article"
---

# icat - kitty

# icat[¶](#icat "Link to this heading")

*Display images in the terminal*

The `icat` kitten can be used to display arbitrary images in the *kitty*
terminal. Using it is as simple as:

```
kitten icat image.jpeg
```

It supports all image types supported by [ImageMagick](https://www.imagemagick.org). It even works over SSH. For details, see the
[kitty graphics protocol](../../graphics-protocol/).

You might want to create an alias in your shell’s configuration files:

```
alias icat="kitten icat"
```

Then you can simply use `icat image.png` to view images.

Note

[ImageMagick](https://www.imagemagick.org) must be installed for the
full range of image types. Without it only PNG/JPG/GIF/BMP/TIFF/WEBP are
supported.

Note

kitty’s image display protocol may not work when used within a terminal
multiplexer such as **screen** or **tmux**, depending on
whether the multiplexer has added support for it or not.

The `icat` kitten has various command line arguments to allow it to be used
from inside other programs to display images. In particular, [`--place`](#cmdoption-kitty-kitten-icat-place),
[`--detect-support`](#cmdoption-kitty-kitten-icat-detect-support) and [`--print-window-size`](#cmdoption-kitty-kitten-icat-print-window-size).

If you are trying to integrate icat into a complex program like a file manager
or editor, there are a few things to keep in mind. icat normally works by communicating
over the TTY device, it both writes to and reads from the TTY. So it is
imperative that while it is running the host program does not do any TTY I/O.
Any key presses or other input from the user on the TTY device will be
discarded. If you would instead like to use it just as a backend to generate
the escape codes for image display, you need to pass it options to tell it the
window dimensions, where to place the image in the window and the transfer mode
to use. If you do that, it will not try to communicate with the TTY device at
all. The requisite options are: [`--use-window-size`](#cmdoption-kitty-kitten-icat-use-window-size), [`--place`](#cmdoption-kitty-kitten-icat-place)
and [`--transfer-mode`](#cmdoption-kitty-kitten-icat-transfer-mode), [`--stdin=no`](#cmdoption-kitty-kitten-icat-stdin).
For example, to demonstrate usage without access to the TTY:

```
zsh -c 'setsid kitten icat --stdin=no --use-window-size $COLUMNS,$LINES,3000,2000 --transfer-mode=file myimage.png'
```

Here, `setsid` ensures icat has no access to the TTY device.
The values, 3000, 2000 are made up. They are the window width and height in
pixels, to obtain which access to the TTY is needed.

To be really robust you should consider writing proper support for the
[kitty graphics protocol](../../graphics-protocol/) in the program instead.
Nowadays there are many libraries that have support for it.

## Source code for icat[¶](#source-code-for-icat "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/icat).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten icat [options] image-file-or-url-or-directory ...
```

A cat like utility to display images in the terminal. You can specify multiple image files and/or directories. Directories are scanned recursively for image files. If STDIN is not a terminal, image data will be read from it as well. You can also specify HTTP(S) or FTP URLs which will be automatically downloaded and displayed.

### Options[¶](#options "Link to this heading")

--align <ALIGN>[¶](#cmdoption-kitty-kitten-icat-align "Link to this definition")
:   Horizontal alignment for the displayed image.
    Default: `center`
    Choices: `center`, `left`, `right`

--place <PLACE>[¶](#cmdoption-kitty-kitten-icat-place "Link to this definition")
:   Choose where on the screen to display the image. The image will be scaled to fit into the specified rectangle. The syntax for specifying rectangles is <width>x<height>@<left>x<top>. All measurements are in cells (i.e. cursor positions) with the origin (0, 0) at the top-left corner of the screen. Note that the [`--align`](#cmdoption-kitty-kitten-icat-align) option will horizontally align the image within this rectangle. By default, the image is horizontally centered within the rectangle. Using place will cause the cursor to be positioned at the top left corner of the image, instead of on the line after the image.

--scale-up [=no][¶](#cmdoption-kitty-kitten-icat-scale-up "Link to this definition")
:   When used in combination with [`--place`](#cmdoption-kitty-kitten-icat-place) it will cause images that are smaller than the specified area to be scaled up to use as much of the specified area as possible.

--background <BACKGROUND>[¶](#cmdoption-kitty-kitten-icat-background "Link to this definition")
:   Specify a background color, this will cause transparent images to be composited on top of the specified color.
    Default: `none`

--mirror <MIRROR>[¶](#cmdoption-kitty-kitten-icat-mirror "Link to this definition")
:   Mirror the image about a horizontal or vertical axis or both.
    Default: `none`
    Choices: `both`, `horizontal`, `none`, `vertical`

--clear [=no][¶](#cmdoption-kitty-kitten-icat-clear "Link to this definition")
:   Remove all images currently displayed on the screen. Note that this cannot work with terminal multiplexers such as tmux since only the multiplexer can know the position of the screen.

--transfer-mode <TRANSFER\_MODE>[¶](#cmdoption-kitty-kitten-icat-transfer-mode "Link to this definition")
:   Which mechanism to use to transfer images to the terminal. The default is to auto-detect. file means to use a temporary file, memory means to use shared memory, stream means to send the data via terminal escape codes. Note that if you use the file or memory transfer modes and you are connecting over a remote session then image display will not work.
    Default: `detect`
    Choices: `detect`, `file`, `memory`, `stream`

--detect-support [=no][¶](#cmdoption-kitty-kitten-icat-detect-support "Link to this definition")
:   Detect support for image display in the terminal. If not supported, will exit with exit code 1, otherwise will exit with code 0 and print the supported transfer mode to stderr, which can be used with the [`--transfer-mode`](#cmdoption-kitty-kitten-icat-transfer-mode) option.

--detection-timeout <DETECTION\_TIMEOUT>[¶](#cmdoption-kitty-kitten-icat-detection-timeout "Link to this definition")
:   The amount of time (in seconds) to wait for a response from the terminal, when detecting image display support.
    Default: `10`

--use-window-size <USE\_WINDOW\_SIZE>[¶](#cmdoption-kitty-kitten-icat-use-window-size "Link to this definition")
:   Instead of querying the terminal for the window size, use the specified size, which must be of the format: width\_in\_cells,height\_in\_cells,width\_in\_pixels,height\_in\_pixels

--print-window-size [=no][¶](#cmdoption-kitty-kitten-icat-print-window-size "Link to this definition")
:   Print out the window size as <width>x<height> (in pixels) and quit. This is a convenience method to query the window size if using `kitten icat` from a scripting language that cannot make termios calls.

--stdin <STDIN>[¶](#cmdoption-kitty-kitten-icat-stdin "Link to this definition")
:   Read image data from STDIN. The default is to do it automatically, when STDIN is not a terminal, but you can turn it off or on explicitly, if needed.
    Default: `detect`
    Choices: `detect`, `no`, `yes`

--silent [=no][¶](#cmdoption-kitty-kitten-icat-silent "Link to this definition")
:   Not used, present for legacy compatibility.

--engine <ENGINE>[¶](#cmdoption-kitty-kitten-icat-engine "Link to this definition")
:   The engine used for decoding and processing of images. The default is to use the most appropriate engine. The `builtin` engine uses Go’s native imaging libraries. The `magick` engine uses ImageMagick which requires it to be installed on the system.
    Default: `auto`
    Choices: `auto`, `builtin`, `magick`

--z-index <Z\_INDEX>, -z <Z\_INDEX>[¶](#cmdoption-kitty-kitten-icat-z-index "Link to this definition")
:   Z-index of the image. When negative, text will be displayed on top of the image. Use a double minus for values under the threshold for drawing images under cell background colors. For example, `--1` evaluates as -1,073,741,825.
    Default: `0`

--loop <LOOP>, -l <LOOP>[¶](#cmdoption-kitty-kitten-icat-loop "Link to this definition")
:   Number of times to loop animations. Negative values loop forever. Zero means only the first frame of the animation is displayed. Otherwise, the animation is looped the specified number of times.
    Default: `-1`

--hold [=no][¶](#cmdoption-kitty-kitten-icat-hold "Link to this definition")
:   Wait for a key press before exiting after displaying the images.

--unicode-placeholder [=no][¶](#cmdoption-kitty-kitten-icat-unicode-placeholder "Link to this definition")
:   Use the Unicode placeholder method to display the images. Useful to display images from within full screen terminal programs that do not understand the kitty graphics protocol such as multiplexers or editors. See [Unicode placeholders](../../graphics-protocol/#graphics-unicode-placeholders) for details. Note that when using this method, images placed (with [`--place`](#cmdoption-kitty-kitten-icat-place)) that do not fit on the screen, will get wrapped at the screen edge instead of getting truncated. This wrapping is per line and therefore the image will look like it is interleaved with blank lines.

--passthrough <PASSTHROUGH>[¶](#cmdoption-kitty-kitten-icat-passthrough "Link to this definition")
:   Whether to surround graphics commands with escape sequences that allow them to passthrough programs like tmux. The default is to detect when running inside tmux and automatically use the tmux passthrough escape codes. Note that when this option is enabled it implies [`--unicode-placeholder`](#cmdoption-kitty-kitten-icat-unicode-placeholder) as well.
    Default: `detect`
    Choices: `detect`, `none`, `tmux`

--image-id <IMAGE\_ID>[¶](#cmdoption-kitty-kitten-icat-image-id "Link to this definition")
:   The graphics protocol id to use for the created image. Normally, a random id is created if needed. This option allows control of the id. When multiple images are sent, sequential ids starting from the specified id are used. Valid ids are from 1 to 4294967295. Numbers outside this range are automatically wrapped.
    Default: `0`

--no-trailing-newline [=no], -n [=no][¶](#cmdoption-kitty-kitten-icat-no-trailing-newline "Link to this definition")
:   By default, the cursor is moved to the next line after displaying an image. This option, prevents that. Should not be used when catting multiple images. Also has no effect when the [`--place`](#cmdoption-kitty-kitten-icat-place) option is used.
---
source_url: "https://davatorium.github.io/rofi/CONFIG/"
title: "Configuration - Rofi Documentation"
crawl_date: "2025-11-16T15:10:41.668319Z"
selector: "article"
---

# Configuration - Rofi Documentation

# Configuration

> This page does not describe all of **ROFI**'s configuration options, just the
> most common usecase. For the full configuration options, check the manpages.

## Where does the configuration live

Rofi's configurations, custom themes live in `${XDG_CONFIG_HOME}/rofi/`, on
most systems this is `~/.config/rofi/`.

The name of the main configuration file is `config.rasi`. (`~/.config/rofi/config.rasi`).

## Create an empty configuration file

Open `~/.config/rofi/config.rasi` in your favorite text editor and add the
following block:

```
configuration {

}
```

You can now set the options in the `configuration` block.

## Create a configuration file from current setup

If you do not want to start from scratch, or want to migrate from older
configuration format, you can get tell rofi to dumps it configuration:

```
rofi -dump-config > ~/.config/rofi/config.rasi
```

This will have all the possible settings and their current value.
If a value is the default value, the entry will be commented.

For example:

```
configuration {               
/*  modes: "window,run,ssh,drun";*/
/*  font: "mono 12";*/
/*  location: 0;*/
/*  yoffset: 0;*/
/*  xoffset: 0;*/
/*  fixed-num-lines: true;*/
... cut ...
/*  ml-row-down: "ScrollDown";*/                                                                                        
/*  me-select-entry: "MousePrimary";*/                                                                                  
/*  me-accept-entry: "MouseDPrimary";*/                                                                                 
/*  me-accept-custom: "Control+MouseDPrimary";*/ 
}
```

To create a copy of the current theme, you can run:

```
rofi -dump-theme > ~/.config/rofi/current.rasi
```

## Configuration file format

### Encoding

The encoding of the file is utf-8. Both Unix (`\n`) and windows (`\r\n`)
newlines format are supported. But Unix is preferred.

### Comments

C and C++ file comments are supported.

* Anything after `//` and before a newline is considered a comment.
* Everything between `/*` and `*/` is a comment.

Comments can be nested and the C comments can be inline.

The following is valid:

```
// Magic comment.
property: /* comment */ value;
```

However, this is not:

```
prop/*comment*/erty: value;
```

### White space

White space and newlines, like comments, are ignored by the parser.

This:

```
property: name;
```

Is identical to:

```
     property             :
name

;
```

### Data types

**ROFI**'s configuration supports several data formats:

#### String

A string is always surrounded by double quotes (`"`). Between the quotes there
can be any printable character.

For example:

```
 ml-row-down: "ScrollDown";
```

#### Number

An integer may contain any full number.

For example:

```
eh: 2;
```

#### Boolean

Boolean value is either `true` or `false`. This is case-sensitive.

For example:

```
show-icons: true;
```

This is equal to the `-show-icons` option on the commandline, and `show-icons:
false;` is equal to `-no-show-icons`.

#### List

This is not supported by the old configuration system, but can be used in the
**rasi** format.

A list starts with a '[' and ends with a ']'. The entries in the list are
comma-separated. The entry in the list single ASCII words.

```
 combi-modes: [window,drun];
```

For older versions you have :

```
 combi-modes: "window,drun";
```

## Get a list of all possible options

There are 2 ways to get a list of all options:

1. Dump the configuration file explained above. (`rofi -dump-config`)
2. Look at output of `rofi -h`.

To see what values an option support check the manpage, it describes most of
them.

NOTE: not all options might be in the manpage, as options can be added at
run-time. (f.e. by plugins).

## Splitting configuration over multiple files

It is possible to split configuration over multiple files using imports. For
example in `~/.config/rofi/config.rasi`

```
configuration {
}
@import "myConfig"
@theme "MyTheme"
```

Rofi will first parse the config block in `~/.config/rofi/config.rasi`, then
parse `~/.config/rofi/myConfig.rasi` and then load the theme `myTheme`. More
information can be obtained from the **rofi-theme(5)** manpage. Imports can be
nested.
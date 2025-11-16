---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/themes/"
title: "Changing kitty colors - kitty"
crawl_date: "2025-11-16T14:48:21.433172Z"
selector: "article"
---

# Changing kitty colors - kitty

# Changing kitty colors[¶](#changing-kitty-colors "Link to this heading")

The themes kitten allows you to easily change color themes, from a collection of
over three hundred pre-built themes available at [kitty-themes](https://github.com/kovidgoyal/kitty-themes). To use it, simply run:

```
kitten themes
```

[![The themes kitten in action](../../_images/themes.png)](../../_images/themes.png)

The kitten allows you to pick a theme, with live previews of the colors. You can
choose between light and dark themes and search by theme name by just typing a
few characters from the name.

The kitten maintains a list of recently used themes to allow quick switching.

If you want to restore the colors to default, you can do so by choosing the
`Default` theme.

Added in version 0.23.0: The themes kitten

## How it works[¶](#how-it-works "Link to this heading")

A theme in kitty is just a `.conf` file containing kitty settings.
When you select a theme, the kitten simply copies the `.conf` file
to `~/.config/kitty/current-theme.conf` and adds an include for
`current-theme.conf` to `kitty.conf`. It also comments out any
existing color settings in `kitty.conf` so they do not interfere.

Once that’s done, the kitten sends kitty a signal to make it reload its config.

Note

If you want to have some color settings in your `kitty.conf` that the
theme kitten does not override, move them into a separate conf file and
`include` it into kitty.conf. The include should be placed after the
inclusion of `current-theme.conf` so that the settings in it override
conflicting settings from `current-theme.conf`.

## Change color themes automatically when the OS switches between light and dark[¶](#change-color-themes-automatically-when-the-os-switches-between-light-and-dark "Link to this heading")

Added in version 0.38.0.

You can have kitty automatically change its color theme when the OS switches
between dark, light and no-preference modes. In order to do this, run the theme
kitten as normal and at the final screen select the option to save your chosen
theme as either light, dark, or no-preference. Repeat until you have chosen
a theme for each of the three modes. Then, once you restart kitty, it will
automatically use your chosen themes depending on the OS color scheme.

This works by creating three files: `dark-theme.auto.conf`,
`light-theme.auto.conf` and `no-preference-theme.auto.conf` in the
kitty config directory. When these files exist, kitty queries the OS for its color scheme
and uses the appropriate file. Note that the colors in these files override all other
colors, and also all background image settings,
even those specified using the [`kitty --override`](../../invocation/#cmdoption-kitty-override) command line flag.
kitty will also automatically change colors when the OS color scheme changes,
for example, during night/day transitions.

When using these colors, you can still dynamically change colors, but the next
time the OS changes its color mode, any dynamic changes will be overridden.

Note

On the GNOME desktop, the desktop reports the color preference as no-preference
when the “Dark style” is not enabled. So use `no-preference-theme.auto.conf` to
select colors for light mode on GNOME. You can manually enable light style
with `gsettings set org.gnome.desktop.interface color-scheme prefer-light`
in which case GNOME will report the color scheme as light and kitty will use
`light-theme.auto.conf`.

## Using your own themes[¶](#using-your-own-themes "Link to this heading")

You can also create your own themes as `.conf` files. Put them in the
`themes` sub-directory of the [kitty config directory](../../conf/#confloc),
usually, `~/.config/kitty/themes`. The kitten will automatically add them
to the list of themes. You can use this to modify the builtin themes, by giving
the conf file the name `Some theme name.conf` to override the builtin
theme of that name. Here, `Some theme name` is the actual builtin theme name, not
its file name. Note that after doing so you have to run the kitten and
choose that theme once for your changes to be applied.

## Contributing new themes[¶](#contributing-new-themes "Link to this heading")

If you wish to contribute a new theme to the kitty theme repository, start by
going to the [kitty-themes](https://github.com/kovidgoyal/kitty-themes)
repository. [Fork it](https://docs.github.com/en/get-started/quickstart/fork-a-repo), and use the
file [`template.conf`](https://github.com/kovidgoyal/kitty-themes/raw/master/template.conf) as a
template when creating your theme. Once you are satisfied with how it looks,
[submit a pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
to have your theme merged into the [kitty-themes](https://github.com/kovidgoyal/kitty-themes) repository, which will make it
available in this kitten automatically.

## Changing the theme non-interactively[¶](#changing-the-theme-non-interactively "Link to this heading")

You can specify the theme name as an argument when invoking the kitten to have
it change to that theme instantly. For example:

```
kitten themes --reload-in=all Dimmed Monokai
```

Will change the theme to `Dimmed Monokai` in all running kitty instances. See
below for more details on non-interactive operation.

## Source code for themes[¶](#source-code-for-themes "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/themes).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten themes [options] [theme name to switch to]
```

Change the kitty theme. If no theme name is supplied, run interactively, otherwise change the current theme to the specified theme name.

### Options[¶](#options "Link to this heading")

--cache-age <CACHE\_AGE>[¶](#cmdoption-kitty-kitten-themes-cache-age "Link to this definition")
:   Check for new themes only after the specified number of days. A value of zero will always check for new themes. A negative value will never check for new themes, instead raising an error if a local copy of the themes is not available.
    Default: `1`

--reload-in <RELOAD\_IN>[¶](#cmdoption-kitty-kitten-themes-reload-in "Link to this definition")
:   By default, this kitten will signal only the parent kitty instance it is running in to reload its config, after making changes. Use this option to instead either not reload the config at all or in all running kitty instances.
    Default: `parent`
    Choices: `all`, `none`, `parent`

--dump-theme [=no][¶](#cmdoption-kitty-kitten-themes-dump-theme "Link to this definition")
:   When running non-interactively, dump the specified theme to STDOUT instead of changing kitty.conf.
    Default: `false`

--config-file-name <CONFIG\_FILE\_NAME>[¶](#cmdoption-kitty-kitten-themes-config-file-name "Link to this definition")
:   The name or path to the config file to edit. Relative paths are interpreted with respect to the kitty config directory. By default the kitty config file, kitty.conf is edited. This is most useful if you add `include themes.conf` to your kitty.conf and then have the kitten operate only on `themes.conf`, allowing `kitty.conf` to remain unchanged.
    Default: `kitty.conf`
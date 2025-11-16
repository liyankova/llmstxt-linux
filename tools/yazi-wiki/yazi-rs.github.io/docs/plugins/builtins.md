---
source_url: "https://yazi-rs.github.io/docs/plugins/builtins"
title: "Builtins | Yazi"
crawl_date: "2025-11-16T14:56:02.224209Z"
selector: "article"
---

# Builtins | Yazi

* [Plugins (BETA)](/docs/plugins/overview)
* Builtins
Version: 25.5.31

On this page

Yazi comes with useful built-in plugins to help enhance your workflow without extra setup. This page introduces these built-in plugins and their available configuration options.

## `fzf.lua`[​](#fzf "Direct link to fzf")

Integrate the power of [`fzf`](https://github.com/junegunn/fzf) into Yazi, allowing you to swiftly search and navigate through files and directories with fuzzy matching.

Source code: <https://github.com/sxyazi/yazi/blob/main/yazi-plugin/preset/plugins/fzf.lua>

### Usage[​](#usage "Direct link to Usage")

How to invoke fzf:

* Press `z` for quick file subtree navigation within CWD.
* Or, press `z` for quick navigation among selected items, if you are in selection mode.

If you exit fzf with a single-selected file:

* [`reveal`](/docs/configuration/keymap#mgr.reveal) the file.
* Or, [`cd`](/docs/configuration/keymap#mgr.cd) to it if it's a directory.

If you exit fzf with multiple-selected files:

* Select the files chosen by fzf in Yazi.
* Or, deselect the files chosen by fzf in Yazi, if you are in selection mode.

## `zoxide.lua`[​](#zoxide "Direct link to zoxide")

Enhance your experience of historical directories navigation with external shell, through [`zoxide`](https://github.com/ajeetdsouza/zoxide), a smarter `cd`.

Source code: <https://github.com/sxyazi/yazi/blob/main/yazi-plugin/preset/plugins/zoxide.lua>

### Usage[​](#usage-1 "Direct link to Usage")

Click `Z` to launch the interactive zoxide UI. Please ensure that:

1. You have installed the latest version of zoxide.
2. You have installed the latest version of [fzf](https://github.com/junegunn/fzf), which is a dependency of zoxide.
3. You have correctly configured zoxide for your shell according to [its documentation](https://github.com/ajeetdsouza/zoxide?tab=readme-ov-file#installation).

### Options[​](#options "Direct link to Options")

| Option | Description |
| --- | --- |
| `update_db` (bool) | Add the path to zoxide database whenever you switches CWD. |

You can *optionally* change certain options in your `init.lua` like this:

```
-- ~/.config/yazi/init.lua  
require("zoxide"):setup {  
	update_db = true,  
}
```
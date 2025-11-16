---
source_url: "https://yazi-rs.github.io/docs/plugins/runtime"
title: "Runtime | Yazi"
crawl_date: "2025-11-16T14:55:53.320890Z"
selector: "article"
---

# Runtime | Yazi

* [Plugins (BETA)](/docs/plugins/overview)
* Runtime
Version: 25.5.31

On this page

## rt[​](#rt "Direct link to rt")

You can access Yazi's runtime through `rt` to obtain startup parameters, terminal properties, [user preferences](/docs/configuration/yazi), etc.

### `args`[​](#rt.args "Direct link to rt.args")

Command-line arguments passed by the user when launching Yazi.

|  |  |
| --- | --- |
| Type | [`rt::Args`](#rt-args) |

### `term`[​](#rt.term "Direct link to rt.term")

User's terminal emulator properties.

|  |  |
| --- | --- |
| Type | [`rt::Term`](#rt-term) |

### `mgr`[​](#rt.mgr "Direct link to rt.mgr")

User preferences under [[mgr]](/docs/configuration/yazi#mgr).

|  |  |
| --- | --- |
| Type | `table` |

### `plugin`[​](#rt.plugin "Direct link to rt.plugin")

User preferences under [[plugin]](/docs/configuration/yazi#plugin).

|  |  |
| --- | --- |
| Type | [`rt::Plugin`](#rt-plugin) |

### `preview`[​](#rt.preview "Direct link to rt.preview")

User preferences under [[preview]](/docs/configuration/yazi#preview).

|  |  |
| --- | --- |
| Type | `table` |

### `tasks`[​](#rt.tasks "Direct link to rt.tasks")

User preferences under [[tasks]](/docs/configuration/yazi#tasks).

|  |  |
| --- | --- |
| Type | `table` |

## th[​](#th "Direct link to th")

You can access the user's theme and flavor configuration through `th`.

### `mgr`[​](#th.mgr "Direct link to th.mgr")

See [[mgr]](/docs/configuration/theme#mgr).

|  |  |
| --- | --- |
| Type | `table` |

### `tabs`[​](#th.tabs "Direct link to th.tabs")

See [[tabs]](/docs/configuration/theme#tabs).

|  |  |
| --- | --- |
| Type | `table` |

### `mode`[​](#th.mode "Direct link to th.mode")

See [[mode]](/docs/configuration/theme#mode).

|  |  |
| --- | --- |
| Type | `table` |

### `status`[​](#th.status "Direct link to th.status")

See [[status]](/docs/configuration/theme#status).

|  |  |
| --- | --- |
| Type | `table` |

### `which`[​](#th.which "Direct link to th.which")

See [[which]](/docs/configuration/theme#which).

|  |  |
| --- | --- |
| Type | `table` |

### `confirm`[​](#th.confirm "Direct link to th.confirm")

See [[confirm]](/docs/configuration/theme#confirm).

|  |  |
| --- | --- |
| Type | `table` |

### `spot`[​](#th.spot "Direct link to th.spot")

See [[spot]](/docs/configuration/theme#spot).

|  |  |
| --- | --- |
| Type | `table` |

### `notify`[​](#th.notify "Direct link to th.notify")

See [[notify]](/docs/configuration/theme#notify).

|  |  |
| --- | --- |
| Type | `table` |

### `pick`[​](#th.pick "Direct link to th.pick")

See [[pick]](/docs/configuration/theme#pick).

|  |  |
| --- | --- |
| Type | `table` |

### `input`[​](#th.input "Direct link to th.input")

See [[input]](/docs/configuration/theme#input).

|  |  |
| --- | --- |
| Type | `table` |

### `cmp`[​](#th.cmp "Direct link to th.cmp")

See [[cmp]](/docs/configuration/theme#cmp).

|  |  |
| --- | --- |
| Type | `table` |

### `tasks`[​](#th.tasks "Direct link to th.tasks")

See [[tasks]](/docs/configuration/theme#tasks).

|  |  |
| --- | --- |
| Type | `table` |

### `help`[​](#th.help "Direct link to th.help")

See [[help]](/docs/configuration/theme#help).

|  |  |
| --- | --- |
| Type | `table` |

## rt::Args[​](#rt-args "Direct link to rt::Args")

### `entries`[​](#rt-args.entries "Direct link to rt-args.entries")

TODO

### `cwd_file`[​](#rt-args.cwd_file "Direct link to rt-args.cwd_file")

TODO

### `chooser_file`[​](#rt-args.chooser_file "Direct link to rt-args.chooser_file")

TODO

## rt::Term[​](#rt-term "Direct link to rt::Term")

User's terminal emulator properties.

### `light`[​](#rt-term.light "Direct link to rt-term.light")

Whether the terminal is in light mode.

|  |  |
| --- | --- |
| Type | `boolean` |

## rt::Plugin[​](#rt-plugin "Direct link to rt::Plugin")

TODO
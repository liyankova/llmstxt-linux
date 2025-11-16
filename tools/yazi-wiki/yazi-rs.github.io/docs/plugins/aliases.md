---
source_url: "https://yazi-rs.github.io/docs/plugins/aliases"
title: "Aliases | Yazi"
crawl_date: "2025-11-16T14:56:04.374275Z"
selector: "article"
---

# Aliases | Yazi

* [Plugins (BETA)](/docs/plugins/overview)
* Aliases
Version: 25.5.31

On this page

## Origin[​](#origin "Direct link to Origin")

A set of constants representing the origin of a position.

|  |  |
| --- | --- |
| Alias | `"top-left"` | `"top-center"` | `"top-right"` | `"bottom-left"` | `"bottom-center"` | `"bottom-right"` | `"center"` | `"hovered"` |

## Sendable[​](#sendable "Direct link to Sendable")

A value that can be sent across threads. See [Sendable value](/docs/plugins/overview#sendable) for more details.

|  |  |
| --- | --- |
| Alias | `nil` | `boolean` | `number` | `string` | `Url` | `{ [Sendable]: Sendable }` |

## Renderable[​](#renderable "Direct link to Renderable")

An element that can be rendered.

|  |  |
| --- | --- |
| Alias | `Bar` | `Border` | `Clear` | `Gauge` | `Line` | `List` | `Text` |

## AsPos[​](#as-pos "Direct link to AsPos")

A value that can be covariantly treated as a [`Pos`](/docs/plugins/layout#pos).

|  |  |
| --- | --- |
| Alias | `Pos` | `{ [1]: Origin, x: integer?, y: integer?, w: integer?, h: integer? }` |

## AsSpan[​](#as-span "Direct link to AsSpan")

A value that can be covariantly treated as a [`Span`](/docs/plugins/layout#span).

|  |  |
| --- | --- |
| Alias | `string` | `Span` |

## AsLine[​](#as-line "Direct link to AsLine")

A value that can be covariantly treated as a [`Line`](/docs/plugins/layout#line).

|  |  |
| --- | --- |
| Alias | `string` | `Span` | `Line` | `(string|Span|Line)[]` |

## AsText[​](#as-text "Direct link to AsText")

A value that can be covariantly treated as a [`Text`](/docs/plugins/layout#text).

|  |  |
| --- | --- |
| Alias | `string` | `Span` | `Line` | `(string|Span|Line)[]` |

## AsColor[​](#as-color "Direct link to AsColor")

A set of constants representing colors.

|  |  |
| --- | --- |
| Alias | `"black"` | `"white"` | `"red"` | `"lightred"` | `"green"` | `"lightgreen"` | `"yellow"` | `"lightyellow"` | `"blue"` | `"lightblue"` | `"magenta"` | `"lightmagenta"` | `"cyan"` | `"lightcyan"` | `"gray"` | `"darkgray"` | `"reset"` | `string` |
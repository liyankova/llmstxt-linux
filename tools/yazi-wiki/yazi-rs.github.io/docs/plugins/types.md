---
source_url: "https://yazi-rs.github.io/docs/plugins/types"
title: "Types | Yazi"
crawl_date: "2025-11-16T14:55:42.399894Z"
selector: "article"
---

# Types | Yazi

* [Plugins (BETA)](/docs/plugins/overview)
* Types
Version: 25.5.31

On this page

## Url[​](#url "Direct link to Url")

Create a Url:

```
-- regular file  
local url = Url("/root/Downloads/logo.png")  
  
-- `bgm.mp3` from the archive `ost.zip`  
local url = Url("archive:///root/ost.zip#bgm.mp3")
```

### `name`[​](#url.name "Direct link to url.name")

Filename of the url.

|  |  |
| --- | --- |
| Type | `string?` |

### `stem`[​](#url.stem "Direct link to url.stem")

Filename without the extension.

|  |  |
| --- | --- |
| Type | `string?` |

### `frag`[​](#url.frag "Direct link to url.frag")

Url fragment.

Let's say the url `archive:///root/my-archive.zip#1.jpg`, the fragment `1.jpg`.

|  |  |
| --- | --- |
| Type | `string?` |

### `parent`[​](#url.parent "Direct link to url.parent")

Parent directory.

|  |  |
| --- | --- |
| Type | `Self?` |

### `is_regular`[​](#url.is_regular "Direct link to url.is_regular")

Whether the file represented by the url is a regular file.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_search`[​](#is_search "Direct link to is_search")

Whether the file represented by the url is from a search result.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_archive`[​](#url.is_archive "Direct link to url.is_archive")

Whether the file represented by the url is from an archive.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_absolute`[​](#is_absolute "Direct link to is_absolute")

Whether the path represented by the url is absolute.

|  |  |
| --- | --- |
| Type | `boolean` |

### `has_root`[​](#url.has_root "Direct link to url.has_root")

Whether the path represented by the url has a root.

|  |  |
| --- | --- |
| Type | `boolean` |

### `join(self, another)`[​](#url.join "Direct link to url.join")

Join with `another` to create a new url.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| `another` | `Self` | `string` |
| Return | `Self` |

### `starts_with(self, another)`[​](#url.starts_with "Direct link to url.starts_with")

Whether the url starts with `another`.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| `another` | `Self` | `string` |
| Return | `boolean` |

### `ends_with(self, another)`[​](#url.ends_with "Direct link to url.ends_with")

Whether the url ends with `another`.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| `another` | `Self` | `string` |
| Return | `boolean` |

### `strip_prefix(self, another)`[​](#url.strip_prefix "Direct link to url.strip_prefix")

Strips the prefix of `another`.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| `another` | `Self` | `string` |
| Return | `Self` |

### `__eq(self, another)`[​](#url.__eq "Direct link to url.__eq")

Whether the url is equal to `another`.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| `another` | `Self` |
| Return | `boolean` |

### `__tostring(self)`[​](#url.__tostring "Direct link to url.__tostring")

Convert the url to string.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| Return | `string` |

### `__concat(self, another)`[​](#url.__concat "Direct link to url.__concat")

Concatenate the url with `another`.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| `another` | `string` |
| Return | `Self` |

### `__new(value)`[​](#url.__new "Direct link to url.__new")

Make a new url.

| In/Out | Type |
| --- | --- |
| `value` | `string` | `Self` |
| Return | `Self` |

## Cha[​](#cha "Direct link to Cha")

One file's characteristics.

### `is_dir`[​](#cha.is_dir "Direct link to cha.is_dir")

Whether the file is a directory.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_hidden`[​](#cha.is_hidden "Direct link to cha.is_hidden")

Whether the file is hidden.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_link`[​](#cha.is_link "Direct link to cha.is_link")

Whether the file is a symlink.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_orphan`[​](#cha.is_orphan "Direct link to cha.is_orphan")

Whether the file is a bad symlink, which points to a non-existent file.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_dummy`[​](#cha.is_dummy "Direct link to cha.is_dummy")

Whether the file is dummy, which fails to load complete metadata, possibly the filesystem doesn't support it, such as FUSE.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_block`[​](#cha.is_block "Direct link to cha.is_block")

Whether the file is a block device.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_char`[​](#cha.is_char "Direct link to cha.is_char")

Whether the file is a character device.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_fifo`[​](#cha.is_fifo "Direct link to cha.is_fifo")

Whether the file is a FIFO.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_sock`[​](#cha.is_sock "Direct link to cha.is_sock")

Whether the file is a socket.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_exec`[​](#cha.is_exec "Direct link to cha.is_exec")

Whether the file is executable.

|  |  |
| --- | --- |
| Type | `boolean` |

### `is_sticky`[​](#cha.is_sticky "Direct link to cha.is_sticky")

Whether the file has the sticky bit set.

|  |  |
| --- | --- |
| Type | `boolean` |

### `len`[​](#cha.len "Direct link to cha.len")

Length of the file in bytes.

If you want to get the size of a directory, use [`size()`](/docs/plugins/context#fs-file.size) instead.

|  |  |
| --- | --- |
| Type | `integer` |

### `atime`[​](#cha.atime "Direct link to cha.atime")

Accessed time of the file in Unix timestamp.

|  |  |
| --- | --- |
| Type | `integer?` |

### `btime`[​](#cha.btime "Direct link to cha.btime")

Birth time of the file in Unix timestamp.

|  |  |
| --- | --- |
| Type | `integer?` |

### `mtime`[​](#cha.mtime "Direct link to cha.mtime")

Modified time of the file in Unix timestamp.

|  |  |
| --- | --- |
| Type | `integer?` |

### `uid`[​](#cha.uid "Direct link to cha.uid")

User id of the file.

|  |  |
| --- | --- |
| Type | `integer?` |
| Available | Unix-like systems only |

### `gid`[​](#cha.gid "Direct link to cha.gid")

Group id of the file.

|  |  |
| --- | --- |
| Type | `integer?` |
| Available | Unix-like systems only |

### `nlink`[​](#cha.nlink "Direct link to cha.nlink")

Number of hard links to the file.

|  |  |
| --- | --- |
| Type | `integer?` |
| Available | Unix-like systems only |

### `perm(self)`[​](#cha.perm "Direct link to cha.perm")

Unix permission representation, such as `drwxr-xr-x`.

|  |  |
| --- | --- |
| Type | `string?` |
| Available | Unix-like systems only |

## File[​](#file "Direct link to File")

A bare file without any context information. See also [`fs::File`](/docs/plugins/context#fs-file).

### `url`[​](#file.url "Direct link to file.url")

Url of the file.

|  |  |
| --- | --- |
| Type | `Url` |

### `cha`[​](#file.cha "Direct link to file.cha")

Cha of the file.

|  |  |
| --- | --- |
| Type | `Cha` |

### `link_to`[​](#file.link_to "Direct link to file.link_to")

Url of the file points to, if it's a symlink.

|  |  |
| --- | --- |
| Type | `Url?` |

### `name`[​](#file.name "Direct link to file.name")

Name of the file.

|  |  |
| --- | --- |
| Type | `string` |

## Icon[​](#icon "Direct link to Icon")

An icon.

### `text`[​](#icon.text "Direct link to icon.text")

Text of the icon.

|  |  |
| --- | --- |
| Type | `string` |

### `style`[​](#icon.style "Direct link to icon.style")

[Style](/docs/plugins/layout#style) of the icon.

|  |  |
| --- | --- |
| Type | `Style` |

## Error[​](#error "Direct link to Error")

An error.

### `code`[​](#error.code "Direct link to error.code")

Raw error code.

|  |  |
| --- | --- |
| Type | `integer` |

### `__tostring(self)`[​](#error.__tostring "Direct link to error.__tostring")

Convert the error to string.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| Return | `string` |

### `__concat(self, another)`[​](#error.__concat "Direct link to error.__concat")

Concatenate the error with `another`.

| In/Out | Type |
| --- | --- |
| `self` | `Self` |
| `another` | `string` |
| Return | `Error` |

## Window[​](#window "Direct link to Window")

### `rows`[​](#window.rows "Direct link to window.rows")

Number of rows.

|  |  |
| --- | --- |
| Type | `integer` |

### `cols`[​](#window.cols "Direct link to window.cols")

Number of columns.

|  |  |
| --- | --- |
| Type | `integer` |

### `width`[​](#window.width "Direct link to window.width")

Width in pixels.

|  |  |
| --- | --- |
| Type | `integer` |

### `height`[​](#window.height "Direct link to window.height")

Height in pixels.

|  |  |
| --- | --- |
| Type | `integer` |
---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/remote_file/"
title: "Remote files - kitty"
crawl_date: "2025-11-16T14:48:32.103949Z"
selector: "article"
---

# Remote files - kitty

# Remote files[¶](#remote-files "Link to this heading")

*kitty* has the ability to easily *Edit*, *Open* or *Download* files from a
computer into which you are SSHed. In your SSH session run:

```
ls --hyperlink=auto
```

Then hold down `Ctrl`+`Shift` and click the name of the file.

[![Remote file actions](../../_images/remote_file.png)](../../_images/remote_file.png)

Remote file actions[¶](#id1 "Link to this image")

*kitty* will ask you what you want to do with the remote file. You can choose
to *Edit* it in which case kitty will download it and open it locally in your
[`EDITOR`](../../glossary/#envvar-EDITOR). As you make changes to the file, they are automatically
transferred to the remote computer. Note that this happens without needing
to install *any* special software on the server, beyond **ls** that
supports hyperlinks.

See also

See the [edit-in-kitty](../../shell-integration/#edit-file) command

See also

See the [Transfer files](../transfer/) kitten

Added in version 0.19.0.

Note

For best results, use this kitten with the [ssh kitten](../ssh/).
Otherwise, nested SSH sessions are not supported. The kitten will always try to copy
remote files from the first SSH host. This is because, without the ssh
kitten, there is no way for
*kitty* to detect and follow a nested SSH session robustly. Use the
[Transfer files](../transfer/) kitten for such situations.

Note

If you have not setup automatic password-less SSH access, and are not using
the ssh kitten, then, when editing
starts you will be asked to enter your password just once, thereafter the SSH
connection will be re-used.

Similarly, you can choose to save the file to the local computer or download
and open it in its default file handler.
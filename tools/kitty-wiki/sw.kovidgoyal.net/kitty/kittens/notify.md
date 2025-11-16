---
source_url: "https://sw.kovidgoyal.net/kitty/kittens/notify/"
title: "notify - kitty"
crawl_date: "2025-11-16T14:48:56.443177Z"
selector: "article"
---

# notify - kitty

# notify[¶](#notify "Link to this heading")

Show pop-up system notifications.

Added in version 0.36.0: The notify kitten

The `notify` kitten can be used to show pop-up system notifications
from the shell. It even works over SSH. Using it is as simple as:

```
kitten notify "Good morning" Hello world, it is a nice day!
```

To add an icon, use:

```
kitten notify --icon-path /path/to/some/image.png "Good morning" Hello world, it is a nice day!
kitten notify --icon firefox "Good morning" Hello world, it is a nice day!
```

To be informed when the notification is activated:

```
kitten notify --wait-for-completion "Good morning" Hello world, it is a nice day!
```

Then, the kitten will wait till the notification is either closed or activated.
If activated, a `0` is printed to `STDOUT`. You can press the
`Esc` or `Ctrl`+`c` keys to abort, closing the notification.

To add buttons to the notification:

```
kitten notify --wait-for-completion --button One --button Two "Good morning" Hello world, it is a nice day!
```

Tip

Learn about the underlying [Desktop notifications](../../desktop-notifications/) escape code protocol.

## Source code for notify[¶](#source-code-for-notify "Link to this heading")

The source code for this kitten is [available on GitHub](https://github.com/kovidgoyal/kitty/tree/master/kittens/notify).

## Command Line Interface[¶](#command-line-interface "Link to this heading")

```
kitten notify [options] TITLE [BODY ...]
```

Send notifications to the user that are displayed to them via the
desktop environment’s notifications service. Works over SSH as well.

To update an existing notification, specify the identifier of the notification
with the --identifier option. The value should be the same as the identifier specified for
the notification you wish to update.

If no title is specified and an identifier is specified using the --identifier
option, then instead of creating a new notification, an existing notification
with the specified identifier is closed.

### Options[¶](#options "Link to this heading")

--icon <ICON>, -n <ICON>[¶](#cmdoption-kitty-kitten-notify-icon "Link to this definition")
:   The name of the icon to use for the notification. An icon with this name will be searched for on the computer running the terminal emulator. Can be specified multiple times, the first name that is found will be used. Standard names: error, file-manager, help, info, question, system-monitor, text-editor, warn, warning

--icon-path <ICON\_PATH>, -p <ICON\_PATH>[¶](#cmdoption-kitty-kitten-notify-icon-path "Link to this definition")
:   Path to an image file in PNG/JPEG/GIF formats to use as the icon. If both name and path are specified then first the name will be looked for and if not found then the path will be used.

--app-name <APP\_NAME>, -a <APP\_NAME>[¶](#cmdoption-kitty-kitten-notify-app-name "Link to this definition")
:   The application name for the notification.
    Default: `kitten-notify`

--button <BUTTON>, -b <BUTTON>[¶](#cmdoption-kitty-kitten-notify-button "Link to this definition")
:   Add a button with the specified text to the notification. Can be specified multiple times for multiple buttons. If --wait-till-closed is used then the kitten will print the button number to STDOUT if the user clicks a button. 1 for the first button, 2 for the second button and so on.

--urgency <URGENCY>, -u <URGENCY>[¶](#cmdoption-kitty-kitten-notify-urgency "Link to this definition")
:   The urgency of the notification.
    Default: `normal`
    Choices: `critical`, `low`, `normal`

--expire-after <EXPIRE\_AFTER>, -e <EXPIRE\_AFTER>[¶](#cmdoption-kitty-kitten-notify-expire-after "Link to this definition")
:   The duration, for the notification to appear on screen. The default is to use the policy of the OS notification service. A value of `never` means the notification should never expire, however, this may or may not work depending on the policies of the OS notification service. Time is specified in the form NUMBER[SUFFIX] where SUFFIX can be `s` for seconds, `m` for minutes, `h` for hours or `d` for days. Non-integer numbers are allowed. If not specified, seconds is assumed. The notification is guaranteed to be closed automatically after the specified time has elapsed. The notification could be closed before by user action or OS policy.

--sound-name <SOUND\_NAME>, -s <SOUND\_NAME>[¶](#cmdoption-kitty-kitten-notify-sound-name "Link to this definition")
:   The name of the sound to play with the notification. `system` means let the notification system use whatever sound it wants. `silent` means prevent any sound from being played. Any other value is passed to the desktop’s notification system which may or may not honor it.
    Default: `system`

--type <TYPE>, -t <TYPE>[¶](#cmdoption-kitty-kitten-notify-type "Link to this definition")
:   The notification type. Can be any string, it is used by users to create filter rules for notifications, so choose something descriptive of the notification’s purpose.

--identifier <IDENTIFIER>, -i <IDENTIFIER>[¶](#cmdoption-kitty-kitten-notify-identifier "Link to this definition")
:   The identifier of this notification. If a notification with the same identifier is already displayed, it is replaced/updated.

--print-identifier [=no], -P [=no][¶](#cmdoption-kitty-kitten-notify-print-identifier "Link to this definition")
:   Print the identifier for the notification to STDOUT. Useful when not specifying your own identifier via the --identifier option.

--wait-for-completion [=no], --wait-till-closed [=no], -w [=no][¶](#cmdoption-kitty-kitten-notify-wait-for-completion "Link to this definition")
:   Wait until the notification is closed. If the user activates the notification, “0” is printed to STDOUT before quitting. If a button on the notification is pressed the number corresponding to the button is printed to STDOUT. Press the Esc or Ctrl+C keys to close the notification manually.

--only-print-escape-code [=no][¶](#cmdoption-kitty-kitten-notify-only-print-escape-code "Link to this definition")
:   Only print the escape code to STDOUT. Useful if using this kitten as part of a larger application. If this is specified, the --wait-till-closed option will be used for escape code generation, but no actual waiting will be done.

--icon-cache-id <ICON\_CACHE\_ID>, -g <ICON\_CACHE\_ID>[¶](#cmdoption-kitty-kitten-notify-icon-cache-id "Link to this definition")
:   Identifier to use when caching icons in the terminal emulator. Using an identifier means that icon data needs to be transmitted only once using --icon-path. Subsequent invocations will use the cached icon data, at least until the terminal instance is restarted. This is useful if this kitten is being used inside a larger application, with --only-print-escape-code.
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/Quickshell"
title: "Quickshell - Quickshell"
crawl_date: "2025-11-16T14:37:50.325310Z"
selector: ".docslayout"
---

# Quickshell - Quickshell

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [stateDir](#stateDir)
* [clipboardText](#clipboardText)
* [dataDir](#dataDir)
* [screens](#screens)
* [watchFiles](#watchFiles)
* [workingDirectory](#workingDirectory)
* [processId](#processId)
* [shellDir](#shellDir)
* [cacheDir](#cacheDir)
* [configDir](#configDir)
* [shellRoot](#shellRoot)

* [cachePath](#cachePath)
* [configPath](#configPath)
* [dataPath](#dataPath)
* [env](#env)
* [execDetached](#execDetached)
* [iconPath](#iconPath)
* [iconPath](#iconPath)
* [iconPath](#iconPath)
* [inhibitReloadPopup](#inhibitReloadPopup)
* [reload](#reload)
* [shellPath](#shellPath)
* [statePath](#statePath)

* [reloadCompleted](#reloadCompleted)
* [reloadFailed](#reloadFailed)
* [lastWindowClosed](#lastWindowClosed)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [Quickshell](/docs/v0.2.1/types/Quickshell/Quickshell)
 

---

## Quickshell: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell`

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* stateDir  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The per-shell state directory.

  Usually `~/.local/state/quickshell/by-shell/<shell-id>`

  Can be overridden using `//@ pragma StateDir $BASE/path` in the root qml file, where `$BASE`
  corrosponds to `$XDG_STATE_HOME` (usually `~/.local/state`).
* clipboardText  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The system clipboard.

  WARNING

  Under wayland the clipboard will be empty unless a quickshell window is focused.
* dataDir  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The per-shell data directory.

  Usually `~/.local/share/quickshell/by-shell/<shell-id>`

  Can be overridden using `//@ pragma DataDir $BASE/path` in the root qml file, where `$BASE`
  corrosponds to `$XDG_DATA_HOME` (usually `~/.local/share`).
* screens  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[ShellScreen](/docs/v0.2.1/types/Quickshell/ShellScreen)>

  readonly

  All currently connected screens.

  This property updates as connected screens change.

  #### Reusing a window on every screen

  ```
  ShellRoot {
    Variants {
      // see Variants for details
      variants: Quickshell.screens
      PanelWindow {
        property var modelData
        screen: modelData
      }
    }
  }
  ```

  This creates an instance of your window once on every screen.
  As screens are added or removed your window will be created or destroyed on those screens.
* watchFiles  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true then the configuration will be reloaded whenever any files change.
  Defaults to true.
* workingDirectory  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Quickshell’s working directory. Defaults to whereever quickshell was launched from.
* processId  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  Quickshell’s process id.
* shellDir  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The full path to the root directory of your shell.

  The root directory is the folder containing the entrypoint to your shell, often referred
  to as `shell.qml`.
* cacheDir  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The per-shell cache directory.

  Usually `~/.cache/quickshell/by-shell/<shell-id>`
* configDir  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  WARNING

  Deprecated: Renamed to [shellDir](#shellDir) for clarity.
* shellRoot  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  WARNING

  Deprecated: Renamed to [shellDir](#shellDir) for consistency.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* cachePath(path)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  path: [string](https://doc.qt.io/qt-6/qml-string.html)

  Equivalent to `${Quickshell.cacheDir}/${path}`
* configPath(path)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  path: [string](https://doc.qt.io/qt-6/qml-string.html)

  WARNING

  Deprecated: Renamed to [shellPath()](#shellPath) for clarity.
* dataPath(path)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  path: [string](https://doc.qt.io/qt-6/qml-string.html)

  Equivalent to `${Quickshell.dataDir}/${path}`
* env(variable)  : 
  [variant](https://doc.qt.io/qt-6/qml-variant.html)

  variable: [string](https://doc.qt.io/qt-6/qml-string.html)

  Returns the string value of an environment variable or null if it is not set.
* execDetached(context)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  context: 

  Launch a process detached from Quickshell.

  The context parameter can either be a list of command arguments or a JS object with the following fields:

  + `command`: A list containing the command and all its arguments. See [Process.command](/docs/v0.2.1/types/Quickshell.Io/Process#command).
  + `environment`: Changes to make to the process environment. See [Process.environment](/docs/v0.2.1/types/Quickshell.Io/Process#environment).
  + `clearEnvironment`: Removes all variables from the environment if true.
  + `workingDirectory`: The working directory the command should run in.

  WARNING

  This does not run command in a shell. All arguments to the command
  must be in separate values in the list, e.g. `["echo", "hello"]`
  and not `["echo hello"]`.

  Additionally, shell scripts must be run by your shell,
  e.g. `["sh", "script.sh"]` instead of `["script.sh"]` unless the script
  has a shebang.

  NOTE

  You can use `["sh", "-c", <your command>]` to execute your command with
  the system shell.

  This function is equivalent to [Process.startDetached()](/docs/v0.2.1/types/Quickshell.Io/Process#startDetached).
* iconPath(icon)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  icon: [string](https://doc.qt.io/qt-6/qml-string.html)

  Returns a string usable for a [Image.source](https://doc.qt.io/qt-6/qml-qtquick-image.html#source-prop) for a given system icon.

  NOTE

  By default, icons are loaded from the theme selected by the qt platform theme,
  which means they should match with all other qt applications on your system.

  If you want to use a different icon theme, you can put `//@ pragma IconTheme <name>`
  at the top of your root config file or set the `QS_ICON_THEME` variable to the name
  of your icon theme.
* iconPath(icon, check)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  icon: [string](https://doc.qt.io/qt-6/qml-string.html)   check: [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Setting the `check` parameter of `iconPath` to true will return an empty string
  if the icon does not exist, instead of an image showing a missing texture.
* iconPath(icon, fallback)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  icon: [string](https://doc.qt.io/qt-6/qml-string.html)   fallback: [string](https://doc.qt.io/qt-6/qml-string.html)

  Setting the `fallback` parameter of `iconPath` will attempt to load the fallback
  icon if the requested one could not be loaded.
* inhibitReloadPopup()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  When called from [reloadCompleted()](#reloadCompleted) or [reloadFailed()](#reloadFailed), prevents the
  default reload popup from displaying.

  The popup can also be blocked by setting `QS_NO_RELOAD_POPUP=1`.
* reload(hard)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  hard: [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Reload the shell.

  `hard` - perform a hard reload. If this is false, Quickshell will attempt to reuse windows
  that already exist. If true windows will be recreated.

  See [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable) for more information on what can be reloaded and how.
* shellPath(path)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  path: [string](https://doc.qt.io/qt-6/qml-string.html)

  Equivalent to `${Quickshell.configDir}/${path}`
* statePath(path)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  path: [string](https://doc.qt.io/qt-6/qml-string.html)

  Equivalent to `${Quickshell.stateDir}/${path}`

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* reloadCompleted()

  The reload sequence has completed successfully.
* reloadFailed(errorString)

  errorString: [string](https://doc.qt.io/qt-6/qml-string.html)

  The reload sequence has failed.
* lastWindowClosed()

  Sent when the last window is closed.

  To make the application exit when the last window is closed run `Qt.quit()`.

* [stateDir](#stateDir)
* [clipboardText](#clipboardText)
* [dataDir](#dataDir)
* [screens](#screens)
* [watchFiles](#watchFiles)
* [workingDirectory](#workingDirectory)
* [processId](#processId)
* [shellDir](#shellDir)
* [cacheDir](#cacheDir)
* [configDir](#configDir)
* [shellRoot](#shellRoot)

* [cachePath](#cachePath)
* [configPath](#configPath)
* [dataPath](#dataPath)
* [env](#env)
* [execDetached](#execDetached)
* [iconPath](#iconPath)
* [iconPath](#iconPath)
* [iconPath](#iconPath)
* [inhibitReloadPopup](#inhibitReloadPopup)
* [reload](#reload)
* [shellPath](#shellPath)
* [statePath](#statePath)

* [reloadCompleted](#reloadCompleted)
* [reloadFailed](#reloadFailed)
* [lastWindowClosed](#lastWindowClosed)
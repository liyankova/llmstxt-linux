---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/DesktopEntry"
title: "Quickshell - DesktopEntry"
crawl_date: "2025-11-16T14:36:39.177709Z"
selector: ".docslayout"
---

# Quickshell - DesktopEntry

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [startupClass](#startupClass)
* [command](#command)
* [genericName](#genericName)
* [runInTerminal](#runInTerminal)
* [workingDirectory](#workingDirectory)
* [name](#name)
* [actions](#actions)
* [categories](#categories)
* [execString](#execString)
* [icon](#icon)
* [id](#id)
* [keywords](#keywords)
* [noDisplay](#noDisplay)
* [comment](#comment)

* [execute](#execute)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [DesktopEntry](/docs/v0.2.1/types/Quickshell/DesktopEntry)
 

---

## DesktopEntry: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell`

A desktop entry. See [DesktopEntries](/docs/v0.2.1/types/Quickshell/DesktopEntries) for details.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* startupClass  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Initial class or app id the app intends to use. May be useful for matching running apps
  to desktop entries.
* command  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[string](https://doc.qt.io/qt-6/qml-string.html)>

  The parsed `Exec` command in the desktop entry.

  The entry can be run with [execute()](#execute), or by using this command in
  [Quickshell.execDetached()](/docs/v0.2.1/types/Quickshell/Quickshell#execDetached) or [Process](/docs/v0.2.1/types/Quickshell.Io/Process).
  If used in `execDetached` or a `Process`, [workingDirectory](#workingDirectory) should also be passed to
  the invoked process. See [execute()](#execute) for details.

  NOTE

  The provided command does not invoke a terminal even if [runInTerminal](#runInTerminal) is true.
* genericName  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Short description of the application, such as “Web Browser”. May be empty.
* runInTerminal  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the application should run in a terminal.
* workingDirectory  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The working directory to execute from.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  *No details provided*
* actions  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[DesktopAction](/docs/v0.2.1/types/Quickshell/DesktopAction)>

  readonly

  *No details provided*
* categories  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[string](https://doc.qt.io/qt-6/qml-string.html)>

  *No details provided*
* execString  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The raw `Exec` string from the desktop entry.

  WARNING

  This cannot be reliably run as a command. See [command](#command) for one you can run.
* icon  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Name of the icon associated with this application. May be empty.
* id  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* keywords  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[string](https://doc.qt.io/qt-6/qml-string.html)>

  *No details provided*
* noDisplay  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true, this application should not be displayed in menus and launchers.
* comment  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Long description of the application, such as “View websites on the internet”. May be empty.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* execute()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Run the application. Currently ignores [runInTerminal](#runInTerminal) and field codes.

  This is equivalent to calling [Quickshell.execDetached()](/docs/v0.2.1/types/Quickshell/Quickshell#execDetached) with [command](#command)
  and [DesktopEntry.workingDirectory](/docs/v0.2.1/types/Quickshell/DesktopEntry#workingDirectory) as shown below:

  ```
  Quickshell.execDetached({
    command: desktopEntry.command,
    workingDirectory: desktopEntry.workingDirectory,
  });
  ```

* [startupClass](#startupClass)
* [command](#command)
* [genericName](#genericName)
* [runInTerminal](#runInTerminal)
* [workingDirectory](#workingDirectory)
* [name](#name)
* [actions](#actions)
* [categories](#categories)
* [execString](#execString)
* [icon](#icon)
* [id](#id)
* [keywords](#keywords)
* [noDisplay](#noDisplay)
* [comment](#comment)

* [execute](#execute)
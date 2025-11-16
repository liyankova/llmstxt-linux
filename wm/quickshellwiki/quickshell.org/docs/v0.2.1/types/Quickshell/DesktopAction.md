---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/DesktopAction"
title: "Quickshell - DesktopAction"
crawl_date: "2025-11-16T14:36:32.657537Z"
selector: ".docslayout"
---

# Quickshell - DesktopAction

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [name](#name)
* [id](#id)
* [command](#command)
* [icon](#icon)
* [execString](#execString)

* [execute](#execute)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [DesktopAction](/docs/v0.2.1/types/Quickshell/DesktopAction)
 

---

## DesktopAction: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell`

An action of a [DesktopEntry](/docs/v0.2.1/types/Quickshell/DesktopEntry).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  *No details provided*
* id  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* command  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[string](https://doc.qt.io/qt-6/qml-string.html)>

  The parsed `Exec` command in the action.

  The entry can be run with [execute()](#execute), or by using this command in
  [Quickshell.execDetached()](/docs/v0.2.1/types/Quickshell/Quickshell#execDetached) or [Process](/docs/v0.2.1/types/Quickshell.Io/Process).
  If used in `execDetached` or a `Process`, [DesktopEntry.workingDirectory](/docs/v0.2.1/types/Quickshell/DesktopEntry#workingDirectory) should also be passed to
  the invoked process.

  NOTE

  The provided command does not invoke a terminal even if [runInTerminal](#runInTerminal) is true.
* icon  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  *No details provided*
* execString  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The raw `Exec` string from the action.

  WARNING

  This cannot be reliably run as a command. See [command](#command) for one you can run.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* execute()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Run the application. Currently ignores [DesktopEntry.runInTerminal](/docs/v0.2.1/types/Quickshell/DesktopEntry#runInTerminal) and field codes.

  This is equivalent to calling [Quickshell.execDetached()](/docs/v0.2.1/types/Quickshell/Quickshell#execDetached) with [command](#command)
  and [DesktopEntry.workingDirectory](/docs/v0.2.1/types/Quickshell/DesktopEntry#workingDirectory).

* [name](#name)
* [id](#id)
* [command](#command)
* [icon](#icon)
* [execString](#execString)

* [execute](#execute)
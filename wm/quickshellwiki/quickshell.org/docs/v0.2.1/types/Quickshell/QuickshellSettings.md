---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/QuickshellSettings"
title: "Quickshell - QuickshellSettings"
crawl_date: "2025-11-16T14:37:54.177045Z"
selector: ".docslayout"
---

# Quickshell - QuickshellSettings

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [workingDirectory](#workingDirectory)
* [watchFiles](#watchFiles)

* [lastWindowClosed](#lastWindowClosed)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [QuickshellSettings](/docs/v0.2.1/types/Quickshell/QuickshellSettings)
 

---

## QuickshellSettings: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell`

Accessor for some options under the Quickshell type. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* workingDirectory  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Quickshell’s working directory. Defaults to whereever quickshell was launched from.
* watchFiles  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true then the configuration will be reloaded whenever any files change.
  Defaults to true.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* lastWindowClosed()

  Sent when the last window is closed.

  To make the application exit when the last window is closed run `Qt.quit()`.

* [workingDirectory](#workingDirectory)
* [watchFiles](#watchFiles)

* [lastWindowClosed](#lastWindowClosed)
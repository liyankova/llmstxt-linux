---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/FileViewError"
title: "Quickshell.Io - FileViewError"
crawl_date: "2025-11-16T14:39:46.168841Z"
selector: ".docslayout"
---

# Quickshell.Io - FileViewError

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [toString](#toString)

* [NotAFile](#NotAFile)
* [PermissionDenied](#PermissionDenied)
* [Success](#Success)
* [FileNotFound](#FileNotFound)
* [Unknown](#Unknown)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [FileViewError](/docs/v0.2.1/types/Quickshell.Io/FileViewError)
 

---

## FileViewError: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

enum

`import Quickshell.Io`

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* toString(value)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  value: [FileViewError](/docs/v0.2.1/types/Quickshell.Io/FileViewError)

  *No details provided*

## Variants

* NotAFile

  The specified path to read/write exists and was not a file.
* PermissionDenied

  Permission to read/write the file was not granted, or permission
  to create parent directories was not granted when writing the file.
* Success

  No error occured.
* FileNotFound

  The file to read does not exist.
* Unknown

  An unknown error occured. Check the logs for details.

* [toString](#toString)

* [NotAFile](#NotAFile)
* [PermissionDenied](#PermissionDenied)
* [Success](#Success)
* [FileNotFound](#FileNotFound)
* [Unknown](#Unknown)
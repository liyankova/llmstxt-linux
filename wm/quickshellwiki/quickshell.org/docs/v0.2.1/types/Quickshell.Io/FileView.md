---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/FileView"
title: "Quickshell.Io - FileView"
crawl_date: "2025-11-16T14:39:40.387452Z"
selector: ".docslayout"
---

# Quickshell.Io - FileView

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [watchChanges](#watchChanges)
* [path](#path)
* [printErrors](#printErrors)
* [blockLoading](#blockLoading)
* [loaded](#loaded)
* [adapter](#adapter)
* [blockAllReads](#blockAllReads)
* [preload](#preload)
* [blockWrites](#blockWrites)
* [atomicWrites](#atomicWrites)

* [data](#data)
* [reload](#reload)
* [setData](#setData)
* [setText](#setText)
* [text](#text)
* [waitForJob](#waitForJob)
* [writeAdapter](#writeAdapter)

* [loaded](#loaded)
* [saveFailed](#saveFailed)
* [saved](#saved)
* [adapterUpdated](#adapterUpdated)
* [fileChanged](#fileChanged)
* [loadFailed](#loadFailed)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [FileView](/docs/v0.2.1/types/Quickshell.Io/FileView)
 

---

## FileView: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell.Io`

A reader for small to medium files that don’t need seeking/cursor access,
suitable for most text files.

#### Example: Reading a JSON as text

```
FileView {
  id: jsonFile
  path: Qt.resolvedUrl("./your.json")
  // Forces the file to be loaded by the time we call JSON.parse().
  // see blockLoading's property documentation for details.
  blockLoading: true
}

readonly property var jsonData: JSON.parse(jsonFile.text())
```

Also see [JsonAdapter](/docs/v0.2.1/types/Quickshell.Io/JsonAdapter) for an alternative way to handle reading and writing JSON files.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* watchChanges  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true (defaule false), [fileChanged()](#fileChanged) will be called whenever the content of the file
  changes on disk, including when [setText()](#setText) or [setData()](#setData) are used.

  NOTE

  You can reload the file’s content whenever it changes on disk like so:

  ```
  FileView {
    // ...
    watchChanges: true
    onFileChanged: this.reload()
  }
  ```
* path  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The path to the file that should be read, or an empty string to unload the file.
* printErrors  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true (default), read or write errors will be printed to the quickshell logs.
  If false, all known errors will not be printed.
* blockLoading  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If [text()](#text) and [data()](#data) should block all operations until the file is loaded. Defaults to false.

  If the file is already loaded, no blocking will occur.
  If a file was loaded, and [path](#path) was changed to a new file, no blocking will occur.

  WARNING

  Blocking operations should be used carefully to avoid stutters and other performance
  degradations. Blocking means that your interface **WILL NOT FUNCTION** during the call.

  **We recommend you use a blocking load ONLY for files loaded before the windows of your shell
  are loaded, which happens after `Component.onCompleted` runs for the root component of your shell.**

  The most reasonable use case would be to load things like configuration files that the program
  must have available.
* loaded  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If a file is currently loaded, which may or may not be the one currently specified by [path](#path).

  NOTE

  If a file is loaded, [path](#path) is changed, and a new file is loaded,
  this property will stay true the whole time.
  If [path](#path) is set to an empty string to unload the file it will become false.
* adapter  : 
  [FileViewAdapter](/docs/v0.2.1/types/Quickshell.Io/FileViewAdapter)

  default

  In addition to directly reading/writing the file as text, *adapters* can be used to
  expose a file’s content in new ways.

  An adapter will automatically be given the loaded file’s content.
  Its state may be saved with [writeAdapter()](#writeAdapter).

  Currently the only adapter is [JsonAdapter](/docs/v0.2.1/types/Quickshell.Io/JsonAdapter).
* blockAllReads  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If [text()](#text) and [data()](#data) should block all operations while a file loads. Defaults to false.

  This is nearly identical to [blockLoading](#blockLoading), but will additionally block when
  a file is loaded and [path](#path) changes.

  WARNING

  We cannot think of a valid use case for this.
  You almost definitely want [blockLoading](#blockLoading).
* preload  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the file should be loaded in the background immediately when set. Defaults to true.

  This may either increase or decrease the amount of time it takes to load the file
  depending on how large the file is, how fast its storage is, and how you access its data.
* blockWrites  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true (default false), all calls to [setText()](#setText) or [setData()](#setData) will block the
  UI thread until the write succeeds or fails.

  WARNING

  Blocking operations should be used carefully to avoid stutters and other performance
  degradations. Blocking means that your interface **WILL NOT FUNCTION** during the call.
* atomicWrites  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true (default), all calls to [setText()](#setText) or [setData()](#setData) will be performed atomically,
  meaning if the write fails for any reason, the file will not be modified.

  NOTE

  This works by creating another file with the desired content, and renaming
  it over the existing file if successful.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* data()  : 
  [unknown](#unknown)

  Returns the data of the file specified by [path](#path) as an [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer).

  If [blockAllReads](#blockAllReads) is true, all changes to [path](#path) will cause the program to block
  when this function is called.

  If [blockLoading](#blockLoading) is true, reading this property before the file has been loaded
  will block, but changing [path](#path) or calling [reload()](#reload) will return the old data
  until the load completes.

  If neither is true, an empty buffer will be returned if no file is loaded,
  otherwise it will behave as in the case above.

  NOTE

  Due to technical limitations, [data()](#data) could not be a property,
  however you can treat it like a property, it will trigger property updates
  as a property would, and the signal `dataChanged()` is present.
* reload()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Unload the loaded file and reload it, usually in response to changes.

  This will not block if [blockLoading](#blockLoading) is set, only if [blockAllReads](#blockAllReads) is true.
  It acts the same as changing [path](#path) to a new file, except loading the same file.
* setData(data)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  data: 

  Sets the content of the file specified by [path](#path) as an [ArrayBuffer].

  [atomicWrites](#atomicWrites) and [blockWrites](#blockWrites) affect the behavior of this function.

  [saved()](#saved) or [saveFailed()](#saveFailed) will be emitted on completion.
* setText(text)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  text: [string](https://doc.qt.io/qt-6/qml-string.html)

  Sets the content of the file specified by [path](#path) as text.

  [atomicWrites](#atomicWrites) and [blockWrites](#blockWrites) affect the behavior of this function.

  [saved()](#saved) or [saveFailed()](#saveFailed) will be emitted on completion.
* text()  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  Returns the data of the file specified by [path](#path) as text.

  If [blockAllReads](#blockAllReads) is true, all changes to [path](#path) will cause the program to block
  when this function is called.

  If [blockLoading](#blockLoading) is true, reading this property before the file has been loaded
  will block, but changing [path](#path) or calling [reload()](#reload) will return the old data
  until the load completes.

  If neither is true, an empty string will be returned if no file is loaded,
  otherwise it will behave as in the case above.

  NOTE

  Due to technical limitations, [text()](#text) could not be a property,
  however you can treat it like a property, it will trigger property updates
  as a property would, and the signal `textChanged()` is present.
* waitForJob()  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Block all operations until the currently running load completes.

  WARNING

  See [blockLoading](#blockLoading) for an explanation and warning about blocking.
* writeAdapter()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Write the content of the current [adapter](#adapter) to the selected file.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* loaded()

  Emitted if the file was loaded successfully.
* saveFailed(error)

  error: [FileViewError](/docs/v0.2.1/types/Quickshell.Io/FileViewError)

  Emitted if the file failed to save.
* saved()

  Emitted if the file was saved successfully.
* adapterUpdated()

  Emitted when the active [adapter](#adapter)’s data is changed.
* fileChanged()

  Emitted if the file changes on disk and [watchChanges](#watchChanges) is true.
* loadFailed(error)

  error: [FileViewError](/docs/v0.2.1/types/Quickshell.Io/FileViewError)

  Emitted if the file failed to load.

* [watchChanges](#watchChanges)
* [path](#path)
* [printErrors](#printErrors)
* [blockLoading](#blockLoading)
* [loaded](#loaded)
* [adapter](#adapter)
* [blockAllReads](#blockAllReads)
* [preload](#preload)
* [blockWrites](#blockWrites)
* [atomicWrites](#atomicWrites)

* [data](#data)
* [reload](#reload)
* [setData](#setData)
* [setText](#setText)
* [text](#text)
* [waitForJob](#waitForJob)
* [writeAdapter](#writeAdapter)

* [loaded](#loaded)
* [saveFailed](#saveFailed)
* [saved](#saved)
* [adapterUpdated](#adapterUpdated)
* [fileChanged](#fileChanged)
* [loadFailed](#loadFailed)
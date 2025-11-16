---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/StdioCollector"
title: "Quickshell.Io - StdioCollector"
crawl_date: "2025-11-16T14:40:09.582953Z"
selector: ".docslayout"
---

# Quickshell.Io - StdioCollector

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [waitForEnd](#waitForEnd)
* [data](#data)
* [text](#text)

* [streamFinished](#streamFinished)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [StdioCollector](/docs/v0.2.1/types/Quickshell.Io/StdioCollector)
 

---

## StdioCollector: [DataStreamParser](/docs/v0.2.1/types/Quickshell.Io/DataStreamParser)

`import Quickshell.Io`

StdioCollector collects all process output into a buffer exposed as [text](#text) or [data](#data).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* waitForEnd  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If true, [text](#text) and [data](#data) will not be updated until the stream ends. Defaults to true.
* data  : 
  [unknown](#unknown)

  readonly

  The stdio buffer exposed as an [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer). if [waitForEnd](#waitForEnd) is true, this will not change
  until the stream ends.
* text  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The stdio buffer exposed as text. if [waitForEnd](#waitForEnd) is true, this will not change
  until the stream ends.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* streamFinished()

  *No details provided*

* [waitForEnd](#waitForEnd)
* [data](#data)
* [text](#text)

* [streamFinished](#streamFinished)
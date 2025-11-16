---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/SplitParser"
title: "Quickshell.Io - SplitParser"
crawl_date: "2025-11-16T14:40:06.892854Z"
selector: ".docslayout"
---

# Quickshell.Io - SplitParser

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [splitMarker](#splitMarker)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [SplitParser](/docs/v0.2.1/types/Quickshell.Io/SplitParser)
 

---

## SplitParser: [DataStreamParser](/docs/v0.2.1/types/Quickshell.Io/DataStreamParser)

`import Quickshell.Io`

DataStreamParser for delimited data streams. [DataStreamParser.read()](/docs/v0.2.1/types/Quickshell.Io/DataStreamParser#read) is emitted once per delimited chunk of the stream.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* splitMarker  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The delimiter for parsed data. May be multiple characters. Defaults to `\n`.

  If the delimiter is empty read lengths may be arbitrary (whatever is returned by the
  underlying read call.)

* [splitMarker](#splitMarker)
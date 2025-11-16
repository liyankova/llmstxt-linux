---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/Socket"
title: "Quickshell.Io - Socket"
crawl_date: "2025-11-16T14:40:01.517602Z"
selector: ".docslayout"
---

# Quickshell.Io - Socket

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [path](#path)
* [connected](#connected)

* [flush](#flush)
* [write](#write)

* [error](#error)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [Socket](/docs/v0.2.1/types/Quickshell.Io/Socket)
 

---

## Socket: [DataStream](/docs/v0.2.1/types/Quickshell.Io/DataStream)

`import Quickshell.Io`

Unix socket listener. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* path  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The path to connect this socket to when [connected](#connected) is set to true.

  Changing this property will have no effect while the connection is active.
* connected  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Returns if the socket is currently connected.

  Writing to this property will set the target connection state and will not
  update the property immediately. Setting the property to false will begin disconnecting
  the socket, and setting it to true will begin connecting the socket if path is not empty.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* flush()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Flush any queued writes to the socket.
* write(data)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  data: [string](https://doc.qt.io/qt-6/qml-string.html)

  Write data to the socket. Does nothing if not connected.

  Remember to call flush after your last write.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* error(error)

  error: 

  This signal is sent whenever a socket error is encountered.

* [path](#path)
* [connected](#connected)

* [flush](#flush)
* [write](#write)

* [error](#error)
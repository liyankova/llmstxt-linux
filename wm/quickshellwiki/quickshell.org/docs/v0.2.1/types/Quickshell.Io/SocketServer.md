---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/SocketServer"
title: "Quickshell.Io - SocketServer"
crawl_date: "2025-11-16T14:40:04.211558Z"
selector: ".docslayout"
---

# Quickshell.Io - SocketServer

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [active](#active)
* [handler](#handler)
* [path](#path)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [SocketServer](/docs/v0.2.1/types/Quickshell.Io/SocketServer)
 

---

## SocketServer: [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)

`import Quickshell.Io`

#### Example

```
SocketServer {
  active: true
  path: "/path/too/socket.sock"
  handler: Socket {
    onConnectedChanged: {
      console.log(connected ? "new connection!" : "connection dropped!")
    }
    parser: SplitParser {
      onRead: message => console.log(`read message from socket: ${message}`)
    }
  }
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* active  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the socket server is currently active. Defaults to false.

  Setting this to false will destory all active connections and delete
  the socket file on disk.

  If path is empty setting this property will have no effect.
* handler  : 
  [Component](https://doc.qt.io/qt-6/qml-qtqml-component.html)

  Connection handler component. Must creeate a [Socket](/docs/v0.2.1/types/Quickshell.Io/Socket).

  The created socket should not set [connected](#connected) or [path](#path) or the incoming
  socket connection will be dropped (they will be set by the socket server.)
  Setting `connected` to false on the created socket after connection will
  close and delete it.
* path  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The path to create the socket server at.

  Setting this property while the server is active will have no effect.

* [active](#active)
* [handler](#handler)
* [path](#path)
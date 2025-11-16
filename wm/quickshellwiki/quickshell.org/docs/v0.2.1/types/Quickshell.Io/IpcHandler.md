---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/IpcHandler"
title: "Quickshell.Io - IpcHandler"
crawl_date: "2025-11-16T14:39:49.519082Z"
selector: ".docslayout"
---

# Quickshell.Io - IpcHandler

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [target](#target)
* [enabled](#enabled)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [IpcHandler](/docs/v0.2.1/types/Quickshell.Io/IpcHandler)
 

---

## IpcHandler: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell.Io`

Each IpcHandler is registered into a per-instance map by its unique [target](#target).
Functions and properties defined on the IpcHandler can be accessed via `qs ipc`.

#### Handler Functions

IPC handler functions can be called by `qs ipc call` as long as they have at most 10
arguments, and all argument types along with the return type are listed below.

**Argument and return types must be explicitly specified or they will not
be registered.**

##### Arguments

* `string` will be passed to the parameter as is.
* `int` will only accept parameters that can be parsed as an integer.
* `bool` will only accept parameters that are “true”, “false”, or an integer,
  where 0 will be converted to false, and anything else to true.
* `real` will only accept parameters that can be parsed as a number with
  or without a decimal.
* `color` will accept [named colors](https://doc.qt.io/qt-6/qml-color.html#svg-color-reference) or hex strings (RGB, RRGGBB, AARRGGBB) with
  an optional `#` prefix.

##### Return Type

* `void` will return nothing.
* `string` will be returned as is.
* `int` will be converted to a string and returned.
* `bool` will be converted to “true” or “false” and returned.
* `real` will be converted to a string and returned.
* `color` will be converted to a hex string in the form `#AARRGGBB` and returned.

#### Example

The following example creates ipc functions to control and retrieve the appearance
of a Rectangle.

```
FloatingWindow {
  Rectangle {
    id: rect
    anchors.centerIn: parent
    width: 100
    height: 100
    color: "red"
  }

  IpcHandler {
    target: "rect"

    function setColor(color: color): void { rect.color = color; }
    function getColor(): color { return rect.color; }
    function setAngle(angle: real): void { rect.rotation = angle; }
    function getAngle(): real { return rect.rotation; }
    function setRadius(radius: int): void { rect.radius = radius; }
    function getRadius(): int { return rect.radius; }
  }
}
```

The list of registered targets can be inspected using `qs ipc show`.

```
$ qs ipc show
target rect
  function setColor(color: color): void
  function getColor(): color
  function setAngle(angle: real): void
  function getAngle(): real
  function setRadius(radius: int): void
  function getRadius(): int
```

and then invoked using `qs ipc call`.

```
$ qs ipc call rect setColor orange
$ qs ipc call rect setAngle 40.5
$ qs ipc call rect setRadius 30
$ qs ipc call rect getColor
#ffffa500
$ qs ipc call rect getAngle
40.5
$ qs ipc call rect getRadius
30
```

#### Properties

Properties of an IpcHanlder can be read using `qs ipc prop get` as long as they are
of an IPC compatible type. See the table above for compatible types.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* target  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The target this handler should be accessible from.
  Required and must be unique. May be changed at runtime.
* enabled  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the handler should be able to receive calls. Defaults to true.

* [target](#target)
* [enabled](#enabled)
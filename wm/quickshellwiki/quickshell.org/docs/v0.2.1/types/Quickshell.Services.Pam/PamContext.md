---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pam/PamContext"
title: "Quickshell.Services.Pam - PamContext"
crawl_date: "2025-11-16T14:40:47.678993Z"
selector: ".docslayout"
---

# Quickshell.Services.Pam - PamContext

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [configDirectory](#configDirectory)
* [messageIsError](#messageIsError)
* [message](#message)
* [responseVisible](#responseVisible)
* [config](#config)
* [active](#active)
* [responseRequired](#responseRequired)
* [user](#user)

* [abort](#abort)
* [respond](#respond)
* [start](#start)

* [error](#error)
* [completed](#completed)
* [pamMessage](#pamMessage)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pam](/docs/v0.2.1/types/Quickshell.Services.Pam)
6. [PamContext](/docs/v0.2.1/types/Quickshell.Services.Pam/PamContext)
 

---

## PamContext: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell.Services.Pam`

Connection to pam. See [the module documentation](../) for pam configuration advice.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* configDirectory  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The pam configuration directory to use. Defaults to “/etc/pam.d”.

  The configuration directory is resolved relative to the current file if not an absolute path.

  This property may not be set while [active](#active) is true.
* messageIsError  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the last message should be shown as an error.
* message  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The last message sent by pam.
* responseVisible  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the user’s response should be visible. Only valid when [responseRequired](#responseRequired) is true.
* config  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The pam configuration to use. Defaults to “login”.

  The configuration should name a file inside [configDirectory](#configDirectory).

  This property may not be set while [active](#active) is true.
* active  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the pam context is actively performing an authentication.

  Setting this value behaves exactly the same as calling [start()](#start) and [abort()](#abort).
* responseRequired  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If pam currently wants a response.

  Responses can be returned with the [respond()](#respond) function.
* user  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The user to authenticate as. If unset the current user will be used.

  This property may not be set while [active](#active) is true.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* abort()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Abort a running authentication session.
* respond(response)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  response: [string](https://doc.qt.io/qt-6/qml-string.html)

  Respond to pam.

  May not be called unless [responseRequired](#responseRequired) is true.
* start()  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Start an authentication session. Returns if the session was started successfully.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* error(error)

  error: [PamError](/docs/v0.2.1/types/Quickshell.Services.Pam/PamError)

  Emitted if pam fails to perform authentication normally.

  A `completed(PamResult.Error)` will be emitted after this event.
* completed(result)

  result: [PamResult](/docs/v0.2.1/types/Quickshell.Services.Pam/PamResult)

  Emitted whenever authentication completes.
* pamMessage()

  Emitted whenever pam sends a new message, after the change signals for
  `message`, `messageIsError`, and `responseRequired`.

* [configDirectory](#configDirectory)
* [messageIsError](#messageIsError)
* [message](#message)
* [responseVisible](#responseVisible)
* [config](#config)
* [active](#active)
* [responseRequired](#responseRequired)
* [user](#user)

* [abort](#abort)
* [respond](#respond)
* [start](#start)

* [error](#error)
* [completed](#completed)
* [pamMessage](#pamMessage)
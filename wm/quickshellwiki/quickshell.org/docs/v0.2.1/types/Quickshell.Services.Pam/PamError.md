---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pam/PamError"
title: "Quickshell.Services.Pam - PamError"
crawl_date: "2025-11-16T14:40:50.669354Z"
selector: ".docslayout"
---

# Quickshell.Services.Pam - PamError

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [toString](#toString)

* [TryAuthFailed](#TryAuthFailed)
* [StartFailed](#StartFailed)
* [InternalError](#InternalError)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pam](/docs/v0.2.1/types/Quickshell.Services.Pam)
6. [PamError](/docs/v0.2.1/types/Quickshell.Services.Pam/PamError)
 

---

## PamError: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

enum

`import Quickshell.Services.Pam`

See [PamContext.error()](/docs/v0.2.1/types/Quickshell.Services.Pam/PamContext#error).

 

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* toString(value)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  value: [PamError](/docs/v0.2.1/types/Quickshell.Services.Pam/PamError)

  *No details provided*

## Variants

* TryAuthFailed

  Failed to try to authenticate the user.
  This is not the same as the user failing to authenticate.
* StartFailed

  Failed to start the pam session.
* InternalError

  An error occurred inside quickshell’s pam interface.

* [toString](#toString)

* [TryAuthFailed](#TryAuthFailed)
* [StartFailed](#StartFailed)
* [InternalError](#InternalError)
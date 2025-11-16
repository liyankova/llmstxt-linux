---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Greetd/Greetd"
title: "Quickshell.Services.Greetd - Greetd"
crawl_date: "2025-11-16T14:40:12.690012Z"
selector: ".docslayout"
---

# Quickshell.Services.Greetd - Greetd

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [available](#available)
* [user](#user)
* [state](#state)

* [cancelSession](#cancelSession)
* [createSession](#createSession)
* [launch](#launch)
* [launch](#launch)
* [launch](#launch)
* [respond](#respond)

* [authMessage](#authMessage)
* [error](#error)
* [launched](#launched)
* [readyToLaunch](#readyToLaunch)
* [authFailure](#authFailure)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Greetd](/docs/v0.2.1/types/Quickshell.Services.Greetd)
6. [Greetd](/docs/v0.2.1/types/Quickshell.Services.Greetd/Greetd)
 

---

## Greetd: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell.Services.Greetd`

This object provides access to a running greetd instance if present.
With it you can authenticate a user and launch a session.

See [the greetd wiki](https://man.sr.ht/~kennylevinsen/greetd/#setting-up-greetd-with-gtkgreet) for instructions on how to set up a graphical greeter.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* available  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the greetd socket is available.
* user  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The currently authenticating user.
* state  : 
  [GreetdState](/docs/v0.2.1/types/Quickshell.Services.Greetd/GreetdState)

  readonly

  The current state of the greetd connection.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* cancelSession()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Cancel the active greetd session.
* createSession(user)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  user: [string](https://doc.qt.io/qt-6/qml-string.html)

  Create a greetd session for the given user.
* launch(command)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  command: [list](https://doc.qt.io/qt-6/qml-list.html)

  Launch the session, exiting quickshell.
  [state](#state) must be `GreetdState.ReadyToLaunch` to call this function.
* launch(command, environment)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  command: [list](https://doc.qt.io/qt-6/qml-list.html)   environment: [list](https://doc.qt.io/qt-6/qml-list.html)

  Launch the session, exiting quickshell.
  [state](#state) must be `GreetdState.ReadyToLaunch` to call this function.
* launch(command, environment, quit)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  command: [list](https://doc.qt.io/qt-6/qml-list.html)   environment: [list](https://doc.qt.io/qt-6/qml-list.html)   quit: [bool](https://doc.qt.io/qt-6/qml-bool.html)

  Launch the session, exiting quickshell if [quit](#quit) is true.
  [state](#state) must be `GreetdState.ReadyToLaunch` to call this function.

  The [launched](#launched) signal can be used to perform an action after greetd has acknowledged
  the desired session.

  WARNING

  Note that greetd expects the greeter to terminate as soon as possible
  after setting a target session, and waiting too long may lead to unexpected behavior
  such as the greeter restarting.

  Performing animations and such should be done *before* calling [launch](#launch).
* respond(response)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  response: [string](https://doc.qt.io/qt-6/qml-string.html)

  Respond to an authentication message.

  May only be called in response to an [authMessage()](#authMessage) with `responseRequired` set to true.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* authMessage(message, error, responseRequired, echoResponse)

  message: [string](https://doc.qt.io/qt-6/qml-string.html)   error: [bool](https://doc.qt.io/qt-6/qml-bool.html)   responseRequired: [bool](https://doc.qt.io/qt-6/qml-bool.html)   echoResponse: [bool](https://doc.qt.io/qt-6/qml-bool.html)

  An authentication message has been sent by greetd.

  + `message` - the text of the message
  + `error` - if the message should be displayed as an error
  + `responseRequired` - if a response via `respond()` is required for this message
  + `echoResponse` - if the response should be displayed in clear text to the user

  Note that `error` and `responseRequired` are mutually exclusive.

  Errors are sent through `authMessage` when they are recoverable, such as a fingerprint scanner
  not being able to read a finger correctly, while definite failures such as a bad password are
  sent through `authFailure`.
* error(error)

  error: [string](https://doc.qt.io/qt-6/qml-string.html)

  Greetd has encountered an error.
* launched()

  Greetd has acknowledged the launch request and the greeter should quit as soon as possible.

  This signal is sent right before quickshell exits automatically if the launch was not specifically
  requested not to exit. You usually don’t need to use this signal.
* readyToLaunch()

  Authentication has finished successfully and greetd can now launch a session.
* authFailure(message)

  message: [string](https://doc.qt.io/qt-6/qml-string.html)

  Authentication has failed an the session has terminated.

  Usually this is something like a timeout or a failed password entry.

* [available](#available)
* [user](#user)
* [state](#state)

* [cancelSession](#cancelSession)
* [createSession](#createSession)
* [launch](#launch)
* [launch](#launch)
* [launch](#launch)
* [respond](#respond)

* [authMessage](#authMessage)
* [error](#error)
* [launched](#launched)
* [readyToLaunch](#readyToLaunch)
* [authFailure](#authFailure)
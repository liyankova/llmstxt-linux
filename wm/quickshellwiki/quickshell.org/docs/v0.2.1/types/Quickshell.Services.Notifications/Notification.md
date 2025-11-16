---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Notifications/Notification"
title: "Quickshell.Services.Notifications - Notification"
crawl_date: "2025-11-16T14:40:32.765470Z"
selector: ".docslayout"
---

# Quickshell.Services.Notifications - Notification

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [expireTimeout](#expireTimeout)
* [summary](#summary)
* [tracked](#tracked)
* [desktopEntry](#desktopEntry)
* [hasInlineReply](#hasInlineReply)
* [hints](#hints)
* [body](#body)
* [resident](#resident)
* [appName](#appName)
* [id](#id)
* [image](#image)
* [hasActionIcons](#hasActionIcons)
* [transient](#transient)
* [lastGeneration](#lastGeneration)
* [urgency](#urgency)
* [actions](#actions)
* [inlineReplyPlaceholder](#inlineReplyPlaceholder)
* [appIcon](#appIcon)

* [dismiss](#dismiss)
* [expire](#expire)
* [sendInlineReply](#sendInlineReply)

* [closed](#closed)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Notifications](/docs/v0.2.1/types/Quickshell.Services.Notifications)
6. [Notification](/docs/v0.2.1/types/Quickshell.Services.Notifications/Notification)
 

---

## Notification: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.Notifications`

A notification emitted by a NotificationServer.

NOTE

This type is [Retainable](/docs/v0.2.1/types/Quickshell/Retainable). It
can be retained after destruction if necessary.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* expireTimeout  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Time in seconds the notification should be valid for
* summary  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The image associated with this notification, or "" if none.
* tracked  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the notification is tracked by the notification server.

  Setting this property to false is equivalent to calling [dismiss()](#dismiss).
* desktopEntry  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The name of the sender’s desktop entry or "" if none was supplied.
* hasInlineReply  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If true, the notification has an inline reply action.

  A quick reply text field should be displayed and the reply can be sent using [sendInlineReply()](#sendInlineReply).
* hints  : 
  [unknown](#unknown)

  readonly

  All hints sent by the client application as a javascript object.
  Many common hints are exposed via other properties.
* body  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  *No details provided*
* resident  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If true, the notification will not be destroyed after an action is invoked.
* appName  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The sending application’s name.
* id  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  Id of the notification as given to the client.
* image  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  An image associated with the notification.

  This image is often something like a profile picture in instant messaging applications.
* hasActionIcons  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If actions associated with this notification have icons available.

  See [NotificationAction.identifier](/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationAction#identifier) for details.
* transient  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If true, the notification should skip any kind of persistence function like a notification area.
* lastGeneration  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this notification was carried over from the last generation
  when quickshell reloaded.

  Notifications from the last generation will only be emitted
  if [NotificationServer.keepOnReload](/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationServer#keepOnReload) is true.
* urgency  : 
  [NotificationUrgency](/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationUrgency)

  readonly

  *No details provided*
* actions  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[NotificationAction](/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationAction)>

  readonly

  Actions that can be taken for this notification.
* inlineReplyPlaceholder  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The placeholder text/button caption for the inline reply.
* appIcon  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The sending application’s icon. If none was provided, then the icon from an associated
  desktop entry will be retrieved. If none was found then "".

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* dismiss()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Destroy the notification and hint to the remote application that it was
  explicitly closed by the user.
* expire()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Destroy the notification and hint to the remote application that it has
  timed out an expired.
* sendInlineReply(replyText)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  replyText: [string](https://doc.qt.io/qt-6/qml-string.html)

  Send an inline reply to the notification with an inline reply action.

  WARNING

  This method can only be called if
  [hasInlineReply](#hasInlineReply) is true
  and the server has [NotificationServer.inlineReplySupported](/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationServer#inlineReplySupported) set to true.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* closed(reason)

  reason: [NotificationCloseReason](/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationCloseReason)

  Sent when a notification has been closed.

  The notification object will be destroyed as soon as all signal handlers exit.

* [expireTimeout](#expireTimeout)
* [summary](#summary)
* [tracked](#tracked)
* [desktopEntry](#desktopEntry)
* [hasInlineReply](#hasInlineReply)
* [hints](#hints)
* [body](#body)
* [resident](#resident)
* [appName](#appName)
* [id](#id)
* [image](#image)
* [hasActionIcons](#hasActionIcons)
* [transient](#transient)
* [lastGeneration](#lastGeneration)
* [urgency](#urgency)
* [actions](#actions)
* [inlineReplyPlaceholder](#inlineReplyPlaceholder)
* [appIcon](#appIcon)

* [dismiss](#dismiss)
* [expire](#expire)
* [sendInlineReply](#sendInlineReply)

* [closed](#closed)
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationAction"
title: "Quickshell.Services.Notifications - NotificationAction"
crawl_date: "2025-11-16T14:40:35.727296Z"
selector: ".docslayout"
---

# Quickshell.Services.Notifications - NotificationAction

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [text](#text)
* [identifier](#identifier)

* [invoke](#invoke)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Notifications](/docs/v0.2.1/types/Quickshell.Services.Notifications)
6. [NotificationAction](/docs/v0.2.1/types/Quickshell.Services.Notifications/NotificationAction)
 

---

## NotificationAction: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.Notifications`

See [Notification.actions](/docs/v0.2.1/types/Quickshell.Services.Notifications/Notification#actions).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* text  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The localized text that should be displayed on a button.
* identifier  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The identifier of the action.

  When [Notification.hasActionIcons](/docs/v0.2.1/types/Quickshell.Services.Notifications/Notification#hasActionIcons) is true, this property will be an icon name.
  When it is false, this property is irrelevant.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* invoke()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Invoke the action. If [Notification.resident](/docs/v0.2.1/types/Quickshell.Services.Notifications/Notification#resident) is false it will be dismissed.

* [text](#text)
* [identifier](#identifier)

* [invoke](#invoke)
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.SystemTray/SystemTray"
title: "Quickshell.Services.SystemTray - SystemTray"
crawl_date: "2025-11-16T14:41:46.137419Z"
selector: ".docslayout"
---

# Quickshell.Services.SystemTray - SystemTray

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [items](#items)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.SystemTray](/docs/v0.2.1/types/Quickshell.Services.SystemTray)
6. [SystemTray](/docs/v0.2.1/types/Quickshell.Services.SystemTray/SystemTray)
 

---

## SystemTray: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell.Services.SystemTray`

Referencing the SystemTray singleton will make quickshell start tracking
system tray contents, which are updated as the tray changes, and can be
accessed via the [items](#items) property.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* items  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[SystemTrayItem](/docs/v0.2.1/types/Quickshell.Services.SystemTray/SystemTrayItem)>

  readonly

  List of all system tray icons.

* [items](#items)
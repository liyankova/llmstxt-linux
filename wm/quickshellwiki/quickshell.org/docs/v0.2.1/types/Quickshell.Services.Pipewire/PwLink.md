---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLink"
title: "Quickshell.Services.Pipewire - PwLink"
crawl_date: "2025-11-16T14:41:17.805162Z"
selector: ".docslayout"
---

# Quickshell.Services.Pipewire - PwLink

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [id](#id)
* [source](#source)
* [target](#target)
* [state](#state)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pipewire](/docs/v0.2.1/types/Quickshell.Services.Pipewire)
6. [PwLink](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLink)
 

---

## PwLink: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.Pipewire`

Note that there is one link per *channel* of a connection between nodes.
You usually want [PwLinkGroup](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLinkGroup).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* id  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The pipewire object id of the link.

  Mainly useful for debugging. you can inspect the link directly
  with `pw-cli i <id>`.
* source  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  readonly

  The node that is *sending* information. (the source)
* target  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  readonly

  The node that is *receiving* information. (the sink)
* state  : 
  [PwLinkState](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLinkState)

  readonly

  The current state of the link.

  WARNING

  This property is invalid unless the node is bound using [PwObjectTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwObjectTracker).

* [id](#id)
* [source](#source)
* [target](#target)
* [state](#state)
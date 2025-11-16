---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLinkGroup"
title: "Quickshell.Services.Pipewire - PwLinkGroup"
crawl_date: "2025-11-16T14:41:20.394641Z"
selector: ".docslayout"
---

# Quickshell.Services.Pipewire - PwLinkGroup

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [state](#state)
* [source](#source)
* [target](#target)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pipewire](/docs/v0.2.1/types/Quickshell.Services.Pipewire)
6. [PwLinkGroup](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLinkGroup)
 

---

## PwLinkGroup: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.Pipewire`

A group of connections between pipewire nodes, one per source->target pair.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* state  : 
  [PwLinkState](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLinkState)

  readonly

  The current state of the link group.

  WARNING

  This property is invalid unless the node is bound using [PwObjectTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwObjectTracker).
* source  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  readonly

  The node that is *sending* information. (the source)
* target  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  readonly

  The node that is *receiving* information. (the sink)

* [state](#state)
* [source](#source)
* [target](#target)
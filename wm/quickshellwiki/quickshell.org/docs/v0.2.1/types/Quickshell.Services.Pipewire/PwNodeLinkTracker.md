---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNodeLinkTracker"
title: "Quickshell.Services.Pipewire - PwNodeLinkTracker"
crawl_date: "2025-11-16T14:41:32.422769Z"
selector: ".docslayout"
---

# Quickshell.Services.Pipewire - PwNodeLinkTracker

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [linkGroups](#linkGroups)
* [node](#node)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pipewire](/docs/v0.2.1/types/Quickshell.Services.Pipewire)
6. [PwNodeLinkTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNodeLinkTracker)
 

---

## PwNodeLinkTracker: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell.Services.Pipewire`

Tracks all link connections to a given node. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* linkGroups  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[PwLinkGroup](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLinkGroup)>

  readonly

  Link groups connected to the given node.

  If the node is a sink, links which target the node will be tracked.
  If the node is a source, links which source the node will be tracked.
* node  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  The node to track connections to.

* [linkGroups](#linkGroups)
* [node](#node)
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pipewire/Pipewire"
title: "Quickshell.Services.Pipewire - Pipewire"
crawl_date: "2025-11-16T14:40:59.306198Z"
selector: ".docslayout"
---

# Quickshell.Services.Pipewire - Pipewire

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [linkGroups](#linkGroups)
* [defaultAudioSink](#defaultAudioSink)
* [preferredDefaultAudioSink](#preferredDefaultAudioSink)
* [nodes](#nodes)
* [preferredDefaultAudioSource](#preferredDefaultAudioSource)
* [links](#links)
* [defaultAudioSource](#defaultAudioSource)
* [ready](#ready)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pipewire](/docs/v0.2.1/types/Quickshell.Services.Pipewire)
6. [Pipewire](/docs/v0.2.1/types/Quickshell.Services.Pipewire/Pipewire)
 

---

## Pipewire: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell.Services.Pipewire`

Contains links to all pipewire objects. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* linkGroups  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[PwLinkGroup](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLinkGroup)>

  readonly

  All link groups present in pipewire.

  The same as [links](#links) but deduplicated.

  If you already have a node you want to check for connections to,
  use [PwNodeLinkTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNodeLinkTracker) instead of filtering this list.
* defaultAudioSink  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  readonly

  The default audio sink (output) or `null`.

  This is the default sink currently in use by pipewire, and the one applications
  are currently using.

  To set the default sink, use [preferredDefaultAudioSink](#preferredDefaultAudioSink).

  NOTE

  When the default sink changes, this property may breifly become null.
  This depends on your hardware.
* preferredDefaultAudioSink  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  The preferred default audio sink (output) or `null`.

  This is a hint to pipewire telling it which sink should be the default when possible.
  [defaultAudioSink](#defaultAudioSink) may differ when it is not possible for pipewire to pick this node.

  See [defaultAudioSink](#defaultAudioSink) for the current default sink, regardless of preference.
* nodes  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)>

  readonly

  All nodes present in pipewire.

  This list contains every node on the system.
  To find a useful subset, filtering with the following properties may be helpful:

  + [PwNode.isStream](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode#isStream) - if the node is an application or hardware device.
  + [PwNode.isSink](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode#isSink) - if the node is a sink or source.
  + [PwNode.audio](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode#audio) - if non null the node is an audio node.
* preferredDefaultAudioSource  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  The preferred default audio source (input) or `null`.

  This is a hint to pipewire telling it which source should be the default when possible.
  [defaultAudioSource](#defaultAudioSource) may differ when it is not possible for pipewire to pick this node.

  See [defaultAudioSource](#defaultAudioSource) for the current default source, regardless of preference.
* links  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[PwLink](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwLink)>

  readonly

  All links present in pipewire.

  Links connect pipewire nodes to each other, and can be used to determine
  their relationship.

  If you already have a node you want to check for connections to,
  use [PwNodeLinkTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNodeLinkTracker) instead of filtering this list.

  NOTE

  Multiple links may exist between the same nodes. See [linkGroups](#linkGroups)
  for a deduplicated list containing only one entry per link between nodes.
* defaultAudioSource  : 
  [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)

  readonly

  The default audio source (input) or `null`.

  This is the default source currently in use by pipewire, and the one applications
  are currently using.

  To set the default source, use [preferredDefaultAudioSource](#preferredDefaultAudioSource).

  NOTE

  When the default source changes, this property may breifly become null.
  This depends on your hardware.
* ready  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  This property is true if quickshell has completed its initial sync with
  the pipewire server. If true, nodes, links and sync/source preferences will be
  in a good state.

  NOTE

  You can use the pipewire object before it is ready, but some nodes/links
  may be missing, and preference metadata may be null.

* [linkGroups](#linkGroups)
* [defaultAudioSink](#defaultAudioSink)
* [preferredDefaultAudioSink](#preferredDefaultAudioSink)
* [nodes](#nodes)
* [preferredDefaultAudioSource](#preferredDefaultAudioSource)
* [links](#links)
* [defaultAudioSource](#defaultAudioSource)
* [ready](#ready)
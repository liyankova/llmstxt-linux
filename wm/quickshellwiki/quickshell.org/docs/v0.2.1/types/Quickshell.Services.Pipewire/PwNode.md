---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode"
title: "Quickshell.Services.Pipewire - PwNode"
crawl_date: "2025-11-16T14:41:26.077431Z"
selector: ".docslayout"
---

# Quickshell.Services.Pipewire - PwNode

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [id](#id)
* [description](#description)
* [nickname](#nickname)
* [isStream](#isStream)
* [ready](#ready)
* [audio](#audio)
* [name](#name)
* [isSink](#isSink)
* [type](#type)
* [properties](#properties)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pipewire](/docs/v0.2.1/types/Quickshell.Services.Pipewire)
6. [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode)
 

---

## PwNode: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.Pipewire`

A node in the pipewire connection graph. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* id  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The pipewire object id of the node.

  Mainly useful for debugging. You can inspect the node directly
  with `pw-cli i <id>`.
* description  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The node’s description, corrosponding to the object’s `node.description` property.

  May be empty. Generally more human readable than [name](#name).
* nickname  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The node’s nickname, corrosponding to the object’s `node.nickname` property.

  May be empty. Generally but not always more human readable than [description](#description).
* isStream  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If `true` then the node is likely to be a program, if `false` it is likely to be
  a hardware device.
* ready  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  True if the node is fully bound and ready to use.

  NOTE

  The node may be used before it is fully bound, but some data
  may be missing or incorrect.
* audio  : 
  [PwNodeAudio](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNodeAudio)

  readonly

  Extra information present only if the node sends or receives audio.

  The presence or absence of this property can be used to determine if a node
  manages audio, regardless of if it is bound. If non null, the node is an audio node.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The node’s name, corrosponding to the object’s `node.name` property.
* isSink  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If `true`, then the node accepts audio input from other nodes,
  if `false` the node outputs audio to other nodes.
* type  : 
  [unknown](#unknown)

  readonly

  The type of this node. Reflects Pipewire’s [media.class](https://docs.pipewire.org/page_man_pipewire-props_7.html).
* properties  : 
  [unknown](#unknown)

  readonly

  The property set present on the node, as an object containing key-value pairs.
  You can inspect this directly with `pw-cli i <id>`.

  A few properties of note, which may or may not be present:

  + `application.name` - A suggested human readable name for the node.
  + `application.icon-name` - The name of an icon recommended to display for the node.
  + `media.name` - A description of the currently playing media.
    (more likely to be present than `media.title` and `media.artist`)
  + `media.title` - The title of the currently playing media.
  + `media.artist` - The artist of the currently playing media.

  WARNING

  This property is invalid unless the node is bound using [PwObjectTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwObjectTracker).

* [id](#id)
* [description](#description)
* [nickname](#nickname)
* [isStream](#isStream)
* [ready](#ready)
* [audio](#audio)
* [name](#name)
* [isSink](#isSink)
* [type](#type)
* [properties](#properties)
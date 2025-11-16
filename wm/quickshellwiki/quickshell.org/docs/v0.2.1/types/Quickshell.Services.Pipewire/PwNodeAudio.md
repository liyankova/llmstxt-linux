---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNodeAudio"
title: "Quickshell.Services.Pipewire - PwNodeAudio"
crawl_date: "2025-11-16T14:41:29.485318Z"
selector: ".docslayout"
---

# Quickshell.Services.Pipewire - PwNodeAudio

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [volume](#volume)
* [channels](#channels)
* [muted](#muted)
* [volumes](#volumes)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.Pipewire](/docs/v0.2.1/types/Quickshell.Services.Pipewire)
6. [PwNodeAudio](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNodeAudio)
 

---

## PwNodeAudio: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.Pipewire`

Extra properties of a [PwNode](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode) if the node is an audio node.

See [PwNode.audio](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwNode#audio).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* volume  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The average volume over all channels of the node.
  Setting this property modifies the volume of all channels proportionately.

  WARNING

  This property is invalid unless the node is bound using [PwObjectTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwObjectTracker).
* channels  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[PwAudioChannel](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwAudioChannel)>

  readonly

  The audio channels present on the node.

  WARNING

  This property is invalid unless the node is bound using [PwObjectTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwObjectTracker).
* muted  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the node is currently muted. Setting this property changes the mute state.

  WARNING

  This property is invalid unless the node is bound using [PwObjectTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwObjectTracker).
* volumes  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[real](https://doc.qt.io/qt-6/qml-real.html)>

  The volumes of each audio channel individually. Each entry corrosponds to
  the volume of the channel at the same index in [channels](#channels). [volumes](#volumes) and [channels](#channels)
  will always be the same length.

  WARNING

  This property is invalid unless the node is bound using [PwObjectTracker](/docs/v0.2.1/types/Quickshell.Services.Pipewire/PwObjectTracker).

* [volume](#volume)
* [channels](#channels)
* [muted](#muted)
* [volumes](#volumes)
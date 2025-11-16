---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/PersistentProperties"
title: "Quickshell - PersistentProperties"
crawl_date: "2025-11-16T14:37:14.858759Z"
selector: ".docslayout"
---

# Quickshell - PersistentProperties

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [reloaded](#reloaded)
* [loaded](#loaded)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [PersistentProperties](/docs/v0.2.1/types/Quickshell/PersistentProperties)
 

---

## PersistentProperties: [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)

`import Quickshell`

PersistentProperties holds properties declated in it across a reload, which is
often useful for things like keeping expandable popups open and styling them.

Below is an example of using `PersistentProperties` to keep track of the state
of an expandable panel. When the configuration is reloaded, the `expanderOpen` property
will be saved and the expandable panel will stay in the open/closed state.

```
PersistentProperties {
  id: persist
  reloadableId: "persistedStates"

  property bool expanderOpen: false
}

Button {
  id: expanderButton
  anchors.centerIn: parent
  text: "toggle expander"
  onClicked: persist.expanderOpen = !persist.expanderOpen
}

Rectangle {
  anchors.top: expanderButton.bottom
  anchors.left: expanderButton.left
  anchors.right: expanderButton.right
  height: 100

  color: "lightblue"
  visible: persist.expanderOpen
}
```

 

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* reloaded()

  Called every time the properties are reloaded.
  Will not be called if no old instance was loaded.
* loaded()

  Called every time the reload stage completes.
  Will be called every time, including when nothing was loaded from an old instance.

* [reloaded](#reloaded)
* [loaded](#loaded)
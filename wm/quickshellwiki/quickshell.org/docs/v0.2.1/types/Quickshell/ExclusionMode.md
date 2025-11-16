---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/ExclusionMode"
title: "Quickshell - ExclusionMode"
crawl_date: "2025-11-16T14:36:52.404953Z"
selector: ".docslayout"
---

# Quickshell - ExclusionMode

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [Ignore](#Ignore)
* [Auto](#Auto)
* [Normal](#Normal)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [ExclusionMode](/docs/v0.2.1/types/Quickshell/ExclusionMode)
 

---

## ExclusionMode: ExclusionMode

`import Quickshell`

See [PanelWindow.exclusionMode](/docs/v0.2.1/types/Quickshell/PanelWindow#exclusionMode).

 

## Variants

* Ignore

  Ignore exclusion zones of other shell layers. You cannot set an exclusion zone in this mode.
* Auto

  Decide the exclusion zone based on the window dimensions and anchors.

  Will attempt to reseve exactly enough space for the window and its margins if
  exactly 3 anchors are connected.
* Normal

  Respect the exclusion zone of other shell layers and optionally set one

* [Ignore](#Ignore)
* [Auto](#Auto)
* [Normal](#Normal)
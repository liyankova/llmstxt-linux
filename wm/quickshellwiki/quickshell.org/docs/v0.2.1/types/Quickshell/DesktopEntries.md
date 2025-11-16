---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/DesktopEntries"
title: "Quickshell - DesktopEntries"
crawl_date: "2025-11-16T14:36:35.710701Z"
selector: ".docslayout"
---

# Quickshell - DesktopEntries

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [applications](#applications)

* [byId](#byId)
* [heuristicLookup](#heuristicLookup)

* [applicationsChanged](#applicationsChanged)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [DesktopEntries](/docs/v0.2.1/types/Quickshell/DesktopEntries)
 

---

## DesktopEntries: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell`

Index of desktop entries according to the [desktop entry specification](https://specifications.freedesktop.org/desktop-entry-spec/latest/).

Primarily useful for looking up icons and metadata from an id, as there is
currently no mechanism for usage based sorting of entries and other launcher niceties.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* applications  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[DesktopEntry](/docs/v0.2.1/types/Quickshell/DesktopEntry)>

  readonly

  All desktop entries of type Application that are not Hidden or NoDisplay.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* byId(id)  : 
  [DesktopEntry](/docs/v0.2.1/types/Quickshell/DesktopEntry)

  id: [string](https://doc.qt.io/qt-6/qml-string.html)

  Look up a desktop entry by name. Includes NoDisplay entries. May return null.

  While this function requires an exact match, [heuristicLookup()](#heuristicLookup) will correctly
  find an entry more often and is generally more useful.
* heuristicLookup(name)  : 
  [DesktopEntry](/docs/v0.2.1/types/Quickshell/DesktopEntry)

  name: [string](https://doc.qt.io/qt-6/qml-string.html)

  Look up a desktop entry by name using heuristics. Unlike [byId()](#byId),
  if no exact matches are found this function will try to guess - potentially incorrectly.
  May return null.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* applicationsChanged()

  *No details provided*

* [applications](#applications)

* [byId](#byId)
* [heuristicLookup](#heuristicLookup)

* [applicationsChanged](#applicationsChanged)
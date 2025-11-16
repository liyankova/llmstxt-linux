---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/ObjectRepeater"
title: "Quickshell - ObjectRepeater"
crawl_date: "2025-11-16T14:37:08.143225Z"
selector: ".docslayout"
---

# Quickshell - ObjectRepeater

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [delegate](#delegate)
* [model](#model)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [ObjectRepeater](/docs/v0.2.1/types/Quickshell/ObjectRepeater)
 

---

## ObjectRepeater: [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel)

uncreatable

`import Quickshell`

> [!ERROR]
> Removed in favor of [Instantiator](https://doc.qt.io/qt-6/qml-qtqml-models-instantiator.html)

The ObjectRepeater creates instances of the provided delegate for every entry in the
given model, similarly to a [Repeater](https://doc.qt.io/qt-6/qml-qtquick-repeater.html) but for non visual types.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* delegate  : 
  [Component](https://doc.qt.io/qt-6/qml-qtqml-component.html)

  default

  The delegate component to repeat.

  The delegate is given the same properties as in a Repeater, except `index` which
  is not currently implemented.

  If the model is a `list<T>` or javascript array, a `modelData` property will be
  exposed containing the entry from the model. If the model is a [QAbstractListModel](https://doc.qt.io/qt-6/qabstractlistmodel.html),
  the roles from the model will be exposed.

  Note: [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) has a single role named `modelData` for compatibility with normal lists.
* model  : 
  [variant](https://doc.qt.io/qt-6/qml-variant.html)

  The model providing data to the ObjectRepeater.

  Currently accepted model types are `list<T>` lists, javascript arrays,
  and [QAbstractListModel](https://doc.qt.io/qt-6/qabstractlistmodel.html) derived models, though only one column will be repeated
  from the latter.

  Note: [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) is a [QAbstractListModel](https://doc.qt.io/qt-6/qabstractlistmodel.html) with a single column.

* [delegate](#delegate)
* [model](#model)
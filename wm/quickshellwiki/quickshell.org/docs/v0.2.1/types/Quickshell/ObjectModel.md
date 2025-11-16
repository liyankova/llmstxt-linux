---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/ObjectModel"
title: "Quickshell - ObjectModel"
crawl_date: "2025-11-16T14:37:04.953538Z"
selector: ".docslayout"
---

# Quickshell - ObjectModel

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [values](#values)

* [indexOf](#indexOf)

* [objectRemovedPost](#objectRemovedPost)
* [objectRemovedPre](#objectRemovedPre)
* [objectInsertedPost](#objectInsertedPost)
* [objectInsertedPre](#objectInsertedPre)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel)
 

---

## ObjectModel: ObjectModel

uncreatable

`import Quickshell`

Typed view into a list of objects.

An ObjectModel works as a QML [Data Model](https://doc.qt.io/qt-6/qtquick-modelviewsdata-modelview.html#qml-data-models), allowing efficient interaction with
components that act on models. It has a single role named `modelData`, to match the
behavior of lists.
The same information contained in the list model is available as a normal list
via the `values` property.

#### Differences from a list

Unlike with a list, the following property binding will never be updated when `model[3]` changes.

```
// will not update reactively
property var foo: model[3]
```

You can work around this limitation using the [values](#values) property of the model to view it as a list.

```
// will update reactively
property var foo: model.values[3]
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* values  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)>

  readonly

  The content of the object model, as a QML list.
  The values of this property will always be of the type of the model.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* indexOf(object)  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  object: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  *No details provided*

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* objectRemovedPost(object, index)

  object: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)   index: [int](https://doc.qt.io/qt-6/qml-int.html)

  Sent immediately after an object is removed from the list.
* objectRemovedPre(object, index)

  object: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)   index: [int](https://doc.qt.io/qt-6/qml-int.html)

  Sent immediately before an object is removed from the list.
* objectInsertedPost(object, index)

  object: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)   index: [int](https://doc.qt.io/qt-6/qml-int.html)

  Sent immediately after an object is inserted into the list.
* objectInsertedPre(object, index)

  object: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)   index: [int](https://doc.qt.io/qt-6/qml-int.html)

  Sent immediately before an object is inserted into the list.

* [values](#values)

* [indexOf](#indexOf)

* [objectRemovedPost](#objectRemovedPost)
* [objectRemovedPre](#objectRemovedPre)
* [objectInsertedPost](#objectInsertedPost)
* [objectInsertedPre](#objectInsertedPre)
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/TransformWatcher"
title: "Quickshell - TransformWatcher"
crawl_date: "2025-11-16T14:38:27.420067Z"
selector: ".docslayout"
---

# Quickshell - TransformWatcher

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [b](#b)
* [transform](#transform)
* [commonParent](#commonParent)
* [a](#a)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [TransformWatcher](/docs/v0.2.1/types/Quickshell/TransformWatcher)
 

---

## TransformWatcher: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell`

The TransformWatcher monitors all properties that affect the geometry
of two [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)s relative to eachother.

NOTE

The algorithm responsible for determining the relationship
between `a` and `b` is biased towards `a` being a parent of `b`,
or `a` being closer to the common parent of `a` and `b` than `b`.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* b  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  *No details provided*
* transform  : 
  [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  readonly

  This property is updated whenever the geometry of any item in the path from `a` to `b` changes.

  Its value is undefined, and is intended to trigger an expression update.
* commonParent  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  Known common parent of both `a` and `b`. Defaults to `null`.

  This property can be used to optimize the algorithm that figures out
  the relationship between `a` and `b`. Setting it to something that is not
  a common parent of both `a` and `b` will prevent the path from being determined
  correctly, and setting it to `null` will disable the optimization.
* a  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  *No details provided*

* [b](#b)
* [transform](#transform)
* [commonParent](#commonParent)
* [a](#a)
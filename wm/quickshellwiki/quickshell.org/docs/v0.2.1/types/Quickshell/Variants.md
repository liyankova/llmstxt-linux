---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/Variants"
title: "Quickshell - Variants"
crawl_date: "2025-11-16T14:38:30.098462Z"
selector: ".docslayout"
---

# Quickshell - Variants

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [model](#model)
* [instances](#instances)
* [delegate](#delegate)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [Variants](/docs/v0.2.1/types/Quickshell/Variants)
 

---

## Variants: [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)

`import Quickshell`

Creates and destroys instances of the given component when the given property changes.

`Variants` is similar to [Repeater](https://doc.qt.io/qt-6/qml-qtquick-repeater.html) except it is for *non [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)* objects, and acts as
a reload scope.

Each non duplicate value passed to [model](#model) will create a new instance of
[delegate](#delegate) with a `modelData` property set to that value.

See [Quickshell.screens](/docs/v0.2.1/types/Quickshell/Quickshell#screens) for an example of using `Variants` to create copies of a window per
screen.

WARNING

BUG: Variants currently fails to reload children if the variant set is changed as
it is instantiated. (usually due to a mutation during variant creation)

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* model  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[variant](https://doc.qt.io/qt-6/qml-variant.html)>

  The list of sets of properties to create instances with.
  Each set creates an instance of the component, which are updated when the input sets update.
* instances  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)>

  readonly

  Current instances of the delegate.
* delegate  : 
  [Component](https://doc.qt.io/qt-6/qml-qtqml-component.html)

  default

  The component to create instances of.

  The delegate should define a `modelData` property that will be popuplated with a value
  from the [model](#model).

* [model](#model)
* [instances](#instances)
* [delegate](#delegate)
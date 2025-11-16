---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/Reloadable"
title: "Quickshell - Reloadable"
crawl_date: "2025-11-16T14:38:01.998189Z"
selector: ".docslayout"
---

# Quickshell - Reloadable

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [reloadableId](#reloadableId)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)
 

---

## Reloadable: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell`

Reloadables will attempt to take specific state from previous config revisions if possible.
Some examples are [ProxyWindowBase](/docs/v0.2.1/types/Quickshell/ProxyWindowBase) and [PersistentProperties](/docs/v0.2.1/types/Quickshell/PersistentProperties)

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* reloadableId  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  An additional identifier that can be used to try to match a reloadable object to its
  previous state.

  Simply keeping a stable identifier across config versions (saves) is
  enough to help the reloader figure out which object in the old revision corrosponds to
  this object in the current revision, and facilitate smoother reloading.

  Note that identifiers are scoped, and will try to do the right thing in context.
  For example if you have a [Variants](/docs/v0.2.1/types/Quickshell/Variants) wrapping an object with an identified element inside,
  a scope is created at the variant level.

  ```
  Variants {
    // multiple variants of the same object tree
    variants: [ { foo: 1 }, { foo: 2 } ]

    // any non `Reloadable` object
    QtObject {
      FloatingWindow {
        // this FloatingWindow will now be matched to the same one in the previous
        // widget tree for its variant. "myFloatingWindow" refers to both the variant in
        // `foo: 1` and `foo: 2` for each tree.
        reloadableId: "myFloatingWindow"

        // ...
      }
    }
  }
  ```

* [reloadableId](#reloadableId)
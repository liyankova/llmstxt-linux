---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/Scope"
title: "Quickshell - Scope"
crawl_date: "2025-11-16T14:38:09.023432Z"
selector: ".docslayout"
---

# Quickshell - Scope

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [children](#children)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [Scope](/docs/v0.2.1/types/Quickshell/Scope)
 

---

## Scope: [Reloadable](/docs/v0.2.1/types/Quickshell/Reloadable)

`import Quickshell`

Convenience type equivalent to setting [Reloadable.reloadableId](/docs/v0.2.1/types/Quickshell/Reloadable#reloadableId) for all children.

Note that this does not work for visible [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)s (all widgets).

```
ShellRoot {
  Variants {
    variants: ...

    Scope {
      // everything in here behaves the same as if it was defined
      // directly in `Variants` reload-wise.
    }
  }
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* children  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)>

  default  readonly

  *No details provided*

* [children](#children)
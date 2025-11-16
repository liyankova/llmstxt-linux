---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/RetainableLock"
title: "Quickshell - RetainableLock"
crawl_date: "2025-11-16T14:38:06.669311Z"
selector: ".docslayout"
---

# Quickshell - RetainableLock

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [retained](#retained)
* [locked](#locked)
* [object](#object)

* [aboutToDestroy](#aboutToDestroy)
* [dropped](#dropped)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [RetainableLock](/docs/v0.2.1/types/Quickshell/RetainableLock)
 

---

## RetainableLock: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell`

A RetainableLock provides extra safety and ease of use for locking
[Retainable](/docs/v0.2.1/types/Quickshell/Retainable) objects. A retainable object can be locked by multiple
locks at once, and each lock re-exposes relevant properties
of the retained objects.

#### Example

The code below will keep a retainable object alive for as long as the
RetainableLock exists.

```
RetainableLock {
  object: aRetainableObject
  locked: true
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* retained  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the object is currently in a retained state.
* locked  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the object should be locked.
* object  : 
  [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  The object to lock. Must be [Retainable](/docs/v0.2.1/types/Quickshell/Retainable).

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* aboutToDestroy()

  Rebroadcast of the object’s [Retainable.aboutToDestroy()](/docs/v0.2.1/types/Quickshell/Retainable#aboutToDestroy).
* dropped()

  Rebroadcast of the object’s [Retainable.dropped()](/docs/v0.2.1/types/Quickshell/Retainable#dropped).

* [retained](#retained)
* [locked](#locked)
* [object](#object)

* [aboutToDestroy](#aboutToDestroy)
* [dropped](#dropped)
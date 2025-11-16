---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/Retainable"
title: "Quickshell - Retainable"
crawl_date: "2025-11-16T14:38:04.334662Z"
selector: ".docslayout"
---

# Quickshell - Retainable

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [retained](#retained)

* [forceUnlock](#forceUnlock)
* [lock](#lock)
* [unlock](#unlock)

* [aboutToDestroy](#aboutToDestroy)
* [dropped](#dropped)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [Retainable](/docs/v0.2.1/types/Quickshell/Retainable)
 

---

## Retainable: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell`

Retainable works as an attached property that allows objects to be
kept around (retained) after they would normally be destroyed, which
is especially useful for things like exit transitions.

An object that is retainable will have [Retainable](/docs/v0.2.1/types/Quickshell/Retainable) as an attached property.
All retainable objects will say that they are retainable on their respective
typeinfo pages.

NOTE

Working directly with [Retainable](/docs/v0.2.1/types/Quickshell/Retainable) is often overly complicated and
error prone. For this reason [RetainableLock](/docs/v0.2.1/types/Quickshell/RetainableLock) should
usually be used instead.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* retained  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the object is currently in a retained state.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* forceUnlock()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Forcibly remove all locks, destroying the object.

  [unlock()](#unlock) should usually be preferred.
* lock()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Hold a lock on the object so it cannot be destroyed.

  A counter is used to ensure you can lock the object from multiple places
  and it will not be unlocked until the same number of unlocks as locks have occurred.

  WARNING

  It is easy to forget to unlock a locked object.
  Doing so will create what is effectively a memory leak.

  Using [RetainableLock](/docs/v0.2.1/types/Quickshell/RetainableLock) is recommended as it will help
  avoid this scenario and make misuse more obvious.
* unlock()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Remove a lock on the object. See [lock()](#lock) for more information.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* aboutToDestroy()

  This signal is sent immediately before the object is destroyed.
  At this point destruction cannot be interrupted.
* dropped()

  This signal is sent when the object would normally be destroyed.

  If all signal handlers return and no locks are in place, the object will be destroyed.
  If at least one lock is present the object will be retained until all are removed.

* [retained](#retained)

* [forceUnlock](#forceUnlock)
* [lock](#lock)
* [unlock](#unlock)

* [aboutToDestroy](#aboutToDestroy)
* [dropped](#dropped)
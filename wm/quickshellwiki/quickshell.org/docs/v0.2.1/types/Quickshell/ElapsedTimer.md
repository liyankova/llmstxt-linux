---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/ElapsedTimer"
title: "Quickshell - ElapsedTimer"
crawl_date: "2025-11-16T14:36:49.421147Z"
selector: ".docslayout"
---

# Quickshell - ElapsedTimer

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [elapsed](#elapsed)
* [elapsedMs](#elapsedMs)
* [elapsedNs](#elapsedNs)
* [restart](#restart)
* [restartMs](#restartMs)
* [restartNs](#restartNs)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [ElapsedTimer](/docs/v0.2.1/types/Quickshell/ElapsedTimer)
 

---

## ElapsedTimer: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell`

The ElapsedTimer measures time since its last restart, and is useful
for determining the time between events that don’t supply it.

 

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* elapsed()  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Return the number of seconds since the timer was last
  started or restarted, with nanosecond precision.
* elapsedMs()  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Return the number of milliseconds since the timer was last
  started or restarted.
* elapsedNs()  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Return the number of nanoseconds since the timer was last
  started or restarted.
* restart()  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Restart the timer, returning the number of seconds since
  the timer was last started or restarted, with nanosecond precision.
* restartMs()  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Restart the timer, returning the number of milliseconds since
  the timer was last started or restarted.
* restartNs()  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Restart the timer, returning the number of nanoseconds since
  the timer was last started or restarted.

* [elapsed](#elapsed)
* [elapsedMs](#elapsedMs)
* [elapsedNs](#elapsedNs)
* [restart](#restart)
* [restartMs](#restartMs)
* [restartNs](#restartNs)
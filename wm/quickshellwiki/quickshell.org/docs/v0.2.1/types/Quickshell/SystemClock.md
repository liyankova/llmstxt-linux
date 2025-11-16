---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/SystemClock"
title: "Quickshell - SystemClock"
crawl_date: "2025-11-16T14:38:24.391773Z"
selector: ".docslayout"
---

# Quickshell - SystemClock

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [hours](#hours)
* [precision](#precision)
* [date](#date)
* [seconds](#seconds)
* [enabled](#enabled)
* [minutes](#minutes)

* [Seconds](#Seconds)
* [Minutes](#Minutes)
* [Hours](#Hours)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [SystemClock](/docs/v0.2.1/types/Quickshell/SystemClock)
 

---

## SystemClock: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

enum

`import Quickshell`

SystemClock is a view into the system’s clock.
It updates at hour, minute, or second intervals depending on [precision](#precision).

# Examples

```
SystemClock {
  id: clock
  precision: SystemClock.Seconds
}

Text {
  text: Qt.formatDateTime(clock.date, "hh:mm:ss - yyyy-MM-dd")
}
```

WARNING

Clock updates will trigger within 50ms of the system clock changing,
however this can be either before or after the clock changes (+-50ms). If you
need a date object, use [date](#date) instead of constructing a new one, or the time
of the constructed object could be off by up to a second.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* hours  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The current hour.
* precision  : 
  [SystemClock](/docs/v0.2.1/types/Quickshell/SystemClock)

  The precision the clock should measure at. Defaults to `SystemClock.Seconds`.
* date  : 
  [date](https://doc.qt.io/qt-6/qml-date.html)

  readonly

  The current date and time.

  TIP

  You can use [Qt.formatDateTime()](https://doc.qt.io/qt-6/qml-qtqml-qt.html#formatDateTime-method) to get the time as a string in
  your format of choice.
* seconds  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The current second, or 0 if [precision](#precision) is `SystemClock.Hours` or `SystemClock.Minutes`.
* enabled  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If the clock should update. Defaults to true.

  Setting enabled to false pauses the clock.
* minutes  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  readonly

  The current minute, or 0 if [precision](#precision) is `SystemClock.Hours`.

## Variants

* Seconds

  *No details provided*
* Minutes

  *No details provided*
* Hours

  *No details provided*

* [hours](#hours)
* [precision](#precision)
* [date](#date)
* [seconds](#seconds)
* [enabled](#enabled)
* [minutes](#minutes)

* [Seconds](#Seconds)
* [Minutes](#Minutes)
* [Hours](#Hours)
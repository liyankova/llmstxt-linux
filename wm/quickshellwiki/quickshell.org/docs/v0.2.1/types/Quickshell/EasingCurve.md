---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/EasingCurve"
title: "Quickshell - EasingCurve"
crawl_date: "2025-11-16T14:36:42.880673Z"
selector: ".docslayout"
---

# Quickshell - EasingCurve

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [curve](#curve)

* [interpolate](#interpolate)
* [interpolate](#interpolate)
* [interpolate](#interpolate)
* [valueAt](#valueAt)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [EasingCurve](/docs/v0.2.1/types/Quickshell/EasingCurve)
 

---

## EasingCurve: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell`

Directly accessible easing curve as used in property animations.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* curve  : 
  [EasingCurve](/docs/v0.2.1/types/Quickshell/EasingCurve)

  Easing curve settings. Works exactly the same as
  [PropertyAnimation.easing](https://doc.qt.io/qt-6/qml-qtquick-propertyanimation.html#easing-prop).

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* interpolate(x, a, b)  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  x: [real](https://doc.qt.io/qt-6/qml-real.html)   a: [real](https://doc.qt.io/qt-6/qml-real.html)   b: [real](https://doc.qt.io/qt-6/qml-real.html)

  Interpolates between two values using the given X coordinate.
* interpolate(x, a, b)  : 
  [point](https://doc.qt.io/qt-6/qml-point.html)

  x: [real](https://doc.qt.io/qt-6/qml-real.html)   a: [point](https://doc.qt.io/qt-6/qml-point.html)   b: [point](https://doc.qt.io/qt-6/qml-point.html)

  Interpolates between two points using the given X coordinate.
* interpolate(x, a, b)  : 
  [rect](https://doc.qt.io/qt-6/qml-rect.html)

  x: [real](https://doc.qt.io/qt-6/qml-real.html)   a: [rect](https://doc.qt.io/qt-6/qml-rect.html)   b: [rect](https://doc.qt.io/qt-6/qml-rect.html)

  Interpolates two rects using the given X coordinate.
* valueAt(x)  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  x: [real](https://doc.qt.io/qt-6/qml-real.html)

  Returns the Y value for the given X value on the curve
  from 0.0 to 1.0.

* [curve](#curve)

* [interpolate](#interpolate)
* [interpolate](#interpolate)
* [interpolate](#interpolate)
* [valueAt](#valueAt)
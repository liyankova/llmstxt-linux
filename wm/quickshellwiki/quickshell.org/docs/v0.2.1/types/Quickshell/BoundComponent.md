---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/BoundComponent"
title: "Quickshell - BoundComponent"
crawl_date: "2025-11-16T14:36:26.040503Z"
selector: ".docslayout"
---

# Quickshell - BoundComponent

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [bindValues](#bindValues)
* [implicitHeight](#implicitHeight)
* [sourceComponent](#sourceComponent)
* [source](#source)
* [item](#item)
* [implicitWidth](#implicitWidth)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [BoundComponent](/docs/v0.2.1/types/Quickshell/BoundComponent)
 

---

## BoundComponent: [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

`import Quickshell`

Component loader that allows setting initial properties, primarily useful for
escaping cyclic dependency errors.

Properties defined on the BoundComponent will be applied to its loaded component,
including required properties, and will remain reactive. Functions created with
the names of signal handlers will also be attached to signals of the loaded component.

```
MouseArea {
  required property color color;
  width: 100
  height: 100

  Rectangle {
    anchors.fill: parent
    color: parent.color
  }
}
```

```
BoundComponent {
  source: "MyComponent.qml"

  // this is the same as assigning to `color` on MyComponent if loaded normally.
  property color color: "red";

  // this will be triggered when the `clicked` signal from the MouseArea is sent.
  function onClicked() {
    color = "blue";
  }
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* bindValues  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  If property values should be bound after they are initially set. Defaults to `true`.
* implicitHeight  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  *No details provided*
* sourceComponent  : 
  [Component](https://doc.qt.io/qt-6/qml-qtqml-component.html)

  The source to load, as a Component.
* source  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The source to load, as a Url.
* item  : 
  [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

  readonly

  The loaded component. Will be null until it has finished loading.
* implicitWidth  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  *No details provided*

* [bindValues](#bindValues)
* [implicitHeight](#implicitHeight)
* [sourceComponent](#sourceComponent)
* [source](#source)
* [item](#item)
* [implicitWidth](#implicitWidth)
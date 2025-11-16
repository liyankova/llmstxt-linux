---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/Region"
title: "Quickshell - Region"
crawl_date: "2025-11-16T14:37:57.368305Z"
selector: ".docslayout"
---

# Quickshell - Region

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [regions](#regions)
* [y](#y)
* [height](#height)
* [shape](#shape)
* [x](#x)
* [intersection](#intersection)
* [item](#item)
* [width](#width)

* [childrenChanged](#childrenChanged)
* [changed](#changed)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [Region](/docs/v0.2.1/types/Quickshell/Region)
 

---

## Region: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell`

See [QsWindow.mask](/docs/v0.2.1/types/Quickshell/QsWindow#mask).

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* regions  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[Region](/docs/v0.2.1/types/Quickshell/Region)>

  default  readonly

  Regions to apply on top of this region.

  Regions can be nested to create a more complex region.
  For example this will create a square region with a cutout in the middle.

  ```
  Region {
    width: 100; height: 100;

    Region {
      x: 50; y: 50;
      width: 50; height: 50;
      intersection: Intersection.Subtract
    }
  }
  ```
* y  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Defaults to 0. Does nothing if [item](#item) is set.
* height  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Defaults to 0. Does nothing if [item](#item) is set.
* shape  : 
  [RegionShape](/docs/v0.2.1/types/Quickshell/RegionShape)

  Defaults to `Rect`.
* x  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Defaults to 0. Does nothing if [item](#item) is set.
* intersection  : 
  [Intersection](/docs/v0.2.1/types/Quickshell/Intersection)

  The way this region interacts with its parent region. Defaults to `Combine`.
* item  : 
  [Item](https://doc.qt.io/qt-6/qml-qtquick-item.html)

  The item that determines the geometry of the region.
  `item` overrides [x](#x), [y](#y), [width](#width) and [height](#height).
* width  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Defaults to 0. Does nothing if [item](#item) is set.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* childrenChanged()

  *No details provided*
* changed()

  Triggered when the region’s geometry changes.

  In some cases the region does not update automatically.
  In those cases you can emit this signal manually.

* [regions](#regions)
* [y](#y)
* [height](#height)
* [shape](#shape)
* [x](#x)
* [intersection](#intersection)
* [item](#item)
* [width](#width)

* [childrenChanged](#childrenChanged)
* [changed](#changed)
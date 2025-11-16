---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/QsMenuEntry"
title: "Quickshell - QsMenuEntry"
crawl_date: "2025-11-16T14:37:35.900408Z"
selector: ".docslayout"
---

# Quickshell - QsMenuEntry

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [enabled](#enabled)
* [isSeparator](#isSeparator)
* [text](#text)
* [hasChildren](#hasChildren)
* [checkState](#checkState)
* [icon](#icon)
* [buttonType](#buttonType)

* [display](#display)

* [triggered](#triggered)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [QsMenuEntry](/docs/v0.2.1/types/Quickshell/QsMenuEntry)
 

---

## QsMenuEntry: [QsMenuHandle](/docs/v0.2.1/types/Quickshell/QsMenuHandle)

uncreatable

`import Quickshell`

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* enabled  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  *No details provided*
* isSeparator  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this menu item should be rendered as a separator between other items.

  No other properties have a meaningful value when [isSeparator](#isSeparator) is true.
* text  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Text of the menu item.
* hasChildren  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If this menu item has children that can be accessed through a [QsMenuOpener](/docs/v0.2.1/types/Quickshell/QsMenuOpener).
* checkState  : 
  [unknown](#unknown)

  readonly

  The check state of the checkbox or radiobutton if applicable, as a
  [Qt.CheckState](https://doc.qt.io/qt-6/qt.html#CheckState-enum).
* icon  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Url of the menu item’s icon or `""` if it doesn’t have one.

  This can be passed to [Image.source](https://doc.qt.io/qt-6/qml-qtquick-image.html#source-prop)
  as shown below.

  ```
  Image {
    source: menuItem.icon
    // To get the best image quality, set the image source size to the same size
    // as the rendered image.
    sourceSize.width: width
    sourceSize.height: height
  }
  ```
* buttonType  : 
  [QsMenuButtonType](/docs/v0.2.1/types/Quickshell/QsMenuButtonType)

  readonly

  If this menu item has an associated checkbox or radiobutton.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* display(parentWindow, relativeX, relativeY)  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  parentWindow: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)   relativeX: [int](https://doc.qt.io/qt-6/qml-int.html)   relativeY: [int](https://doc.qt.io/qt-6/qml-int.html)

  Display a platform menu at the given location relative to the parent window.

## Signals [[?]](/docs/v0.2.1guide/qml-language#signals)

* triggered()

  Send a trigger/click signal to the menu entry.

* [enabled](#enabled)
* [isSeparator](#isSeparator)
* [text](#text)
* [hasChildren](#hasChildren)
* [checkState](#checkState)
* [icon](#icon)
* [buttonType](#buttonType)

* [display](#display)

* [triggered](#triggered)
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/ColorQuantizer"
title: "Quickshell - ColorQuantizer"
crawl_date: "2025-11-16T14:36:29.442687Z"
selector: ".docslayout"
---

# Quickshell - ColorQuantizer

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [colors](#colors)
* [depth](#depth)
* [source](#source)
* [rescaleSize](#rescaleSize)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [ColorQuantizer](/docs/v0.2.1/types/Quickshell/ColorQuantizer)
 

---

## ColorQuantizer: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

`import Quickshell`

A color quantization utility used for getting prevalent colors in an image, by
averaging out the image’s color data recursively.

#### Example

```
ColorQuantizer {
  id: colorQuantizer
  source: Qt.resolvedUrl("./yourImage.png")
  depth: 3 // Will produce 8 colors (2³)
  rescaleSize: 64 // Rescale to 64x64 for faster processing
}
```

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* colors  : 
  [list](https://doc.qt.io/qt-6/qml-list.html) <[color](https://doc.qt.io/qt-6/qml-color.html)>

  readonly

  Access the colors resulting from the color quantization performed.

  NOTE

  The amount of colors returned from the quantization is determined by
  the property depth, specifically 2ⁿ where n is the depth.
* depth  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  Max depth for the color quantization. Each level of depth represents another
  binary split of the color space
* source  : 
  [unknown](#unknown)

  Path to the image you’d like to run the color quantization on.
* rescaleSize  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  The size to rescale the image to, when rescaleSize is 0 then no scaling will be done.

  NOTE

  Results from color quantization doesn’t suffer much when rescaling, it’s
  reccommended to rescale, otherwise the quantization process will take much longer.

* [colors](#colors)
* [depth](#depth)
* [source](#source)
* [rescaleSize](#rescaleSize)
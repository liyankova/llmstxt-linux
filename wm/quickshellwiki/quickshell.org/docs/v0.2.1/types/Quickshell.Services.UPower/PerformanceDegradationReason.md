---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.UPower/PerformanceDegradationReason"
title: "Quickshell.Services.UPower - PerformanceDegradationReason"
crawl_date: "2025-11-16T14:41:52.198673Z"
selector: ".docslayout"
---

# Quickshell.Services.UPower - PerformanceDegradationReason

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [toString](#toString)

* [None](#None)
* [LapDetected](#LapDetected)
* [HighTemperature](#HighTemperature)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.UPower](/docs/v0.2.1/types/Quickshell.Services.UPower)
6. [PerformanceDegradationReason](/docs/v0.2.1/types/Quickshell.Services.UPower/PerformanceDegradationReason)
 

---

## PerformanceDegradationReason: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

enum

`import Quickshell.Services.UPower`

See [PowerProfiles.degradationReason](/docs/v0.2.1/types/Quickshell.Services.UPower/PowerProfiles#degradationReason) for more information.

 

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* toString(reason)  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  reason: [PerformanceDegradationReason](/docs/v0.2.1/types/Quickshell.Services.UPower/PerformanceDegradationReason)

  *No details provided*

## Variants

* None

  Performance has not been degraded in a way power-profiles-daemon can detect.
* LapDetected

  Performance has been reduced due to the computer’s lap detection function,
  which attempts to keep the computer from getting too hot while on your lap.
* HighTemperature

  Performance has been reduced due to high system temperatures.

* [toString](#toString)

* [None](#None)
* [LapDetected](#LapDetected)
* [HighTemperature](#HighTemperature)
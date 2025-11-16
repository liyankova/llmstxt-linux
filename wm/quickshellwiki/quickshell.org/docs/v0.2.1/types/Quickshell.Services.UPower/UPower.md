---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.UPower/UPower"
title: "Quickshell.Services.UPower - UPower"
crawl_date: "2025-11-16T14:42:00.508442Z"
selector: ".docslayout"
---

# Quickshell.Services.UPower - UPower

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [devices](#devices)
* [displayDevice](#displayDevice)
* [onBattery](#onBattery)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.UPower](/docs/v0.2.1/types/Quickshell.Services.UPower)
6. [UPower](/docs/v0.2.1/types/Quickshell.Services.UPower/UPower)
 

---

## UPower: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell.Services.UPower`

An interface to the [UPower daemon](https://upower.freedesktop.org), which can be used to
view battery and power statistics for your computer and
connected devices.

NOTE

The UPower daemon must be installed to use this service.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* devices  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[UPowerDevice](/docs/v0.2.1/types/Quickshell.Services.UPower/UPowerDevice)>

  readonly

  All connected UPower devices.
* displayDevice  : 
  [UPowerDevice](/docs/v0.2.1/types/Quickshell.Services.UPower/UPowerDevice)

  readonly

  UPower’s DisplayDevice for your system. Cannot be null,
  but might not be initialized (check [UPowerDevice.ready](/docs/v0.2.1/types/Quickshell.Services.UPower/UPowerDevice#ready) if you need to know).

  This is an aggregate device and not a physical one, meaning you will not find it in [devices](#devices).
  It is typically the device that is used for displaying information in desktop environments.
* onBattery  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the system is currently running on battery power, or discharging.

* [devices](#devices)
* [displayDevice](#displayDevice)
* [onBattery](#onBattery)
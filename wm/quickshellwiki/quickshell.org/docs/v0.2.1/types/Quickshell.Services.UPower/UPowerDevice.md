---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Services.UPower/UPowerDevice"
title: "Quickshell.Services.UPower - UPowerDevice"
crawl_date: "2025-11-16T14:42:03.539442Z"
selector: ".docslayout"
---

# Quickshell.Services.UPower - UPowerDevice

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [energy](#energy)
* [healthPercentage](#healthPercentage)
* [healthSupported](#healthSupported)
* [model](#model)
* [timeToEmpty](#timeToEmpty)
* [changeRate](#changeRate)
* [percentage](#percentage)
* [timeToFull](#timeToFull)
* [type](#type)
* [energyCapacity](#energyCapacity)
* [iconName](#iconName)
* [powerSupply](#powerSupply)
* [isLaptopBattery](#isLaptopBattery)
* [isPresent](#isPresent)
* [nativePath](#nativePath)
* [ready](#ready)
* [state](#state)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Services.UPower](/docs/v0.2.1/types/Quickshell.Services.UPower)
6. [UPowerDevice](/docs/v0.2.1/types/Quickshell.Services.UPower/UPowerDevice)
 

---

## UPowerDevice: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Services.UPower`

A device exposed through the UPower system service. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* energy  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Current energy level of the device in watt-hours.
* healthPercentage  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Health of the device as a percentage of its original health.
* healthSupported  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  *No details provided*
* model  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Model name of the device. Unlikely to be useful for internal devices.
* timeToEmpty  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Estimated time until the device is fully discharged, in seconds.

  Will be set to `0` if charging.
* changeRate  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Rate of energy change in watts (positive when charging, negative when discharging).
* percentage  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Current charge level as a percentage.

  This would be equivalent to [energy](#energy) / [energyCapacity](#energyCapacity).
* timeToFull  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Estimated time until the device is fully charged, in seconds.

  Will be set to `0` if discharging.
* type  : 
  [UPowerDeviceType](/docs/v0.2.1/types/Quickshell.Services.UPower/UPowerDeviceType)

  readonly

  The type of device.
* energyCapacity  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Maximum energy capacity of the device in watt-hours
* iconName  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Name of the icon representing the current state of the device, or an empty string if not provided.
* powerSupply  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the device is a power supply for your computer and can provide charge.
* isLaptopBattery  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the device is a laptop battery or not. Use this to check if your device is a valid battery.

  This will be equivalent to [type](#type) == Battery && [powerSupply](#powerSupply) == true.
* isPresent  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If the power source is present in the bay or slot, useful for hot-removable batteries.

  If the device `type` is not `Battery`, then the property will be invalid.
* nativePath  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  Native path of the device specific to your OS.
* ready  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  If device statistics have been queried for this device yet.
  This will be true for all devices returned from [UPower.devices](/docs/v0.2.1/types/Quickshell.Services.UPower/UPower#devices), but not the default
  device, which may be returned before it is ready to avoid returning null.
* state  : 
  [UPowerDeviceState](/docs/v0.2.1/types/Quickshell.Services.UPower/UPowerDeviceState)

  readonly

  Current state of the device.

* [energy](#energy)
* [healthPercentage](#healthPercentage)
* [healthSupported](#healthSupported)
* [model](#model)
* [timeToEmpty](#timeToEmpty)
* [changeRate](#changeRate)
* [percentage](#percentage)
* [timeToFull](#timeToFull)
* [type](#type)
* [energyCapacity](#energyCapacity)
* [iconName](#iconName)
* [powerSupply](#powerSupply)
* [isLaptopBattery](#isLaptopBattery)
* [isPresent](#isPresent)
* [nativePath](#nativePath)
* [ready](#ready)
* [state](#state)
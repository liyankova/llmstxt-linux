---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothDevice"
title: "Quickshell.Bluetooth - BluetoothDevice"
crawl_date: "2025-11-16T14:38:42.708458Z"
selector: ".docslayout"
---

# Quickshell.Bluetooth - BluetoothDevice

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [trusted](#trusted)
* [bonded](#bonded)
* [adapter](#adapter)
* [name](#name)
* [state](#state)
* [battery](#battery)
* [batteryAvailable](#batteryAvailable)
* [connected](#connected)
* [pairing](#pairing)
* [wakeAllowed](#wakeAllowed)
* [paired](#paired)
* [blocked](#blocked)
* [dbusPath](#dbusPath)
* [address](#address)
* [deviceName](#deviceName)
* [icon](#icon)

* [cancelPair](#cancelPair)
* [connect](#connect)
* [disconnect](#disconnect)
* [forget](#forget)
* [pair](#pair)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Bluetooth](/docs/v0.2.1/types/Quickshell.Bluetooth)
6. [BluetoothDevice](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothDevice)
 

---

## BluetoothDevice: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Bluetooth`

A tracked Bluetooth device. 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* trusted  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the device is considered to be trusted by the system.
  Trusted devices are allowed to reconnect themselves to the system without intervention.
* bonded  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  True if pairing information is stored for future connections.
* adapter  : 
  [BluetoothAdapter](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothAdapter)

  readonly

  The Bluetooth adapter this device belongs to.
* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  The name of the Bluetooth device. This property may be written to create an alias, or set to
  an empty string to fall back to the device provided name.

  See [deviceName](#deviceName) for the name provided by the device.
* state  : 
  [BluetoothDeviceState](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothDeviceState)

  readonly

  Connection state of the device.
* battery  : 
  [real](https://doc.qt.io/qt-6/qml-real.html)

  readonly

  Battery level of the connected device, from `0.0` to `1.0`. Only valid if [batteryAvailable](#batteryAvailable) is true.
* batteryAvailable  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  True if the connected device reports its battery level. Battery level can be accessed via [battery](#battery).
* connected  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the device is currently connected to the computer.

  Setting this property is equivalent to calling [connect()](#connect) and [disconnect()](#disconnect).

  NOTE

  [state](#state) provides more detailed information if required.
* pairing  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  True if the device is currently being paired.

  NOTE

  [cancelPair()](#cancelPair) can be used to cancel the pairing process.
* wakeAllowed  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the device is allowed to wake up the host system from suspend.
* paired  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  readonly

  True if the device is paired to the computer.

  NOTE

  [pair()](#pair) can be used to pair a device, however you must [forget()](#forget) the device to unpair it.
* blocked  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the device is blocked from connecting.
  If a device is blocked, any connection attempts will be immediately rejected by the system.
* dbusPath  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  DBus path of the device under the `org.bluez` system service.
* address  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  MAC address of the device.
* deviceName  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The name of the Bluetooth device, ignoring user provided aliases. See also [name](#name)
  which returns a user provided alias if set.
* icon  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  System icon representing the device type. Use [Quickshell.iconPath()](/docs/v0.2.1/types/Quickshell/Quickshell#iconPath) to display this in an image.

## Functions [[?]](/docs/v0.2.1guide/qml-language#functions)

* cancelPair()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Cancel an active pairing attempt.
* connect()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Attempt to connect to the device.
* disconnect()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Disconnect from the device.
* forget()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Forget the device.
* pair()  : 
  [void](https://doc.qt.io/qt-6/qml-void.html)

  Attempt to pair the device.

  NOTE

  [paired](#paired) and [pairing](#pairing) return the current pairing status of the device.

* [trusted](#trusted)
* [bonded](#bonded)
* [adapter](#adapter)
* [name](#name)
* [state](#state)
* [battery](#battery)
* [batteryAvailable](#batteryAvailable)
* [connected](#connected)
* [pairing](#pairing)
* [wakeAllowed](#wakeAllowed)
* [paired](#paired)
* [blocked](#blocked)
* [dbusPath](#dbusPath)
* [address](#address)
* [deviceName](#deviceName)
* [icon](#icon)

* [cancelPair](#cancelPair)
* [connect](#connect)
* [disconnect](#disconnect)
* [forget](#forget)
* [pair](#pair)
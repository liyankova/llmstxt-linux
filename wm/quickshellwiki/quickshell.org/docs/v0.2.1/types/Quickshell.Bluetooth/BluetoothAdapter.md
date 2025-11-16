---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothAdapter"
title: "Quickshell.Bluetooth - BluetoothAdapter"
crawl_date: "2025-11-16T14:38:35.880503Z"
selector: ".docslayout"
---

# Quickshell.Bluetooth - BluetoothAdapter

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [name](#name)
* [pairable](#pairable)
* [devices](#devices)
* [dbusPath](#dbusPath)
* [discoverableTimeout](#discoverableTimeout)
* [pairableTimeout](#pairableTimeout)
* [state](#state)
* [discoverable](#discoverable)
* [discovering](#discovering)
* [adapterId](#adapterId)
* [enabled](#enabled)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Bluetooth](/docs/v0.2.1/types/Quickshell.Bluetooth)
6. [BluetoothAdapter](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothAdapter)
 

---

## BluetoothAdapter: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

uncreatable

`import Quickshell.Bluetooth`

A Bluetooth adapter 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* name  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  System provided name of the adapter. See [adapterId](#adapterId) for the internal identifier.
* pairable  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the adapter is accepting incoming pairing requests.

  This only affects incoming pairing requests and should typically only be changed
  by system settings applications. Defaults to true.
* devices  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[BluetoothDevice](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothDevice)>

  readonly

  Bluetooth devices connected to this adapter.
* dbusPath  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  DBus path of the adapter under the `org.bluez` system service.
* discoverableTimeout  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Timeout in seconds for how long the adapter stays discoverable after [discoverable](#discoverable) is set to true.
  A value of 0 means the adapter stays discoverable forever.
* pairableTimeout  : 
  [int](https://doc.qt.io/qt-6/qml-int.html)

  Timeout in seconds for how long the adapter stays pairable after [pairable](#pairable) is set to true.
  A value of 0 means the adapter stays pairable forever. Defaults to 0.
* state  : 
  [BluetoothAdapterState](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothAdapterState)

  readonly

  Detailed power state of the adapter.
* discoverable  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the adapter can be discovered by other bluetooth devices.
* discovering  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the adapter is scanning for new devices.
* adapterId  : 
  [string](https://doc.qt.io/qt-6/qml-string.html)

  readonly

  The internal ID of the adapter (e.g., “hci0”).
* enabled  : 
  [bool](https://doc.qt.io/qt-6/qml-bool.html)

  True if the adapter is currently enabled. More detailed state is available from [state](#state).

* [name](#name)
* [pairable](#pairable)
* [devices](#devices)
* [dbusPath](#dbusPath)
* [discoverableTimeout](#discoverableTimeout)
* [pairableTimeout](#pairableTimeout)
* [state](#state)
* [discoverable](#discoverable)
* [discovering](#discovering)
* [adapterId](#adapterId)
* [enabled](#enabled)
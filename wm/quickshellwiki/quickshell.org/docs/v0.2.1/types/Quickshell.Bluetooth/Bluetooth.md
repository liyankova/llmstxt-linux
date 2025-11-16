---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Bluetooth/Bluetooth"
title: "Quickshell.Bluetooth - Bluetooth"
crawl_date: "2025-11-16T14:38:32.746923Z"
selector: ".docslayout"
---

# Quickshell.Bluetooth - Bluetooth

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [adapters](#adapters)
* [defaultAdapter](#defaultAdapter)
* [devices](#devices)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Bluetooth](/docs/v0.2.1/types/Quickshell.Bluetooth)
6. [Bluetooth](/docs/v0.2.1/types/Quickshell.Bluetooth/Bluetooth)
 

---

## Bluetooth: [QtObject](https://doc.qt.io/qt-6/qml-qtqml-qtobject.html)

singleton

`import Quickshell.Bluetooth`

Provides access to bluetooth devices and adapters.

 

## Properties [[?]](/docs/v0.2.1/guide/qml-language#properties)

* adapters  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[BluetoothAdapter](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothAdapter)>

  readonly

  A list of all bluetooth adapters. See [defaultAdapter](#defaultAdapter) for the default.
* defaultAdapter  : 
  [BluetoothAdapter](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothAdapter)

  readonly

  The default bluetooth adapter. Usually there is only one.
* devices  : 
  [ObjectModel](/docs/v0.2.1/types/Quickshell/ObjectModel) <[BluetoothDevice](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothDevice)>

  readonly

  A list of all connected bluetooth devices across all adapters.
  See [BluetoothAdapter.devices](/docs/v0.2.1/types/Quickshell.Bluetooth/BluetoothAdapter#devices) for the devices connected to a single adapter.

* [adapters](#adapters)
* [defaultAdapter](#defaultAdapter)
* [devices](#devices)
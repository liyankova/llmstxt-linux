---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell.Io/JsonAdapter"
title: "Quickshell.Io - JsonAdapter"
crawl_date: "2025-11-16T14:39:52.396136Z"
selector: ".docslayout"
---

# Quickshell.Io - JsonAdapter

### [Quickshell](/)

`CtrlK`   

Cancel

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell.Io](/docs/v0.2.1/types/Quickshell.Io)
6. [JsonAdapter](/docs/v0.2.1/types/Quickshell.Io/JsonAdapter)
 

---

## JsonAdapter: [FileViewAdapter](/docs/v0.2.1/types/Quickshell.Io/FileViewAdapter)

`import Quickshell.Io`

JsonAdapter is a [FileView](/docs/v0.2.1/types/Quickshell.Io/FileView) adapter that exposes a JSON file as a set of QML
properties that can be read and written to.

Each property defined in a JsonAdapter corresponds to a key in the JSON file.
Supported property types are:

* Primitves (`int`, `bool`, `string`, `real`)
* Sub-object adapters ([JsonObject](/docs/v0.2.1/types/Quickshell.Io/JsonObject))
* JSON objects and arrays, as a `var` type
* Lists of any of the above (`list<string>` etc)

When the [FileView](/docs/v0.2.1/types/Quickshell.Io/FileView)’s data is loaded, properties of a JsonAdapter or
sub-object adapter ([JsonObject](/docs/v0.2.1/types/Quickshell.Io/JsonObject)) are updated if their values have changed.

When properties of a JsonAdapter or sub-object adapter are changed from QML,
[FileView.adapterUpdated()](/docs/v0.2.1/types/Quickshell.Io/FileView#adapterUpdated) is emitted, which may be used to save the file’s new
state (see [FileView.writeAdapter()](/docs/v0.2.1/types/Quickshell.Io/FileView#writeAdapter)).

### Example

```
FileView {
  path: "/path/to/file"

  // when changes are made on disk, reload the file's content
  watchChanges: true
  onFileChanged: reload()

  // when changes are made to properties in the adapter, save them
  onAdapterUpdated: writeAdapter()

  JsonAdapter {
    property string myStringProperty: "default value"
    onMyStringPropertyChanged: {
      console.log("myStringProperty was changed via qml or on disk")
    }

    property list<string> stringList: [ "default", "value" ]

    property JsonObject subObject: JsonObject {
      property string subObjectProperty: "default value"
      onSubObjectPropertyChanged: console.log("same as above")
    }

    // works the same way as subObject
    property var inlineJson: { "a": "b" }
  }
}
```

The above snippet produces the JSON document below:

```
{
   "myStringProperty": "default value",
   "stringList": [
     "default",
     "value"
   ],
   "subObject": {
     "subObjectProperty": "default value"
   },
   "inlineJson": {
     "a": "b"
   }
}
```
---
source_url: "https://quickshell.org/docs/v0.2.1/types/Quickshell/Intersection"
title: "Quickshell - Intersection"
crawl_date: "2025-11-16T14:36:58.211861Z"
selector: ".docslayout"
---

# Quickshell - Intersection

### [Quickshell](/)

`CtrlK`   

Cancel

  

* [Combine](#Combine)
* [Xor](#Xor)
* [Subtract](#Subtract)
* [Intersect](#Intersect)

2. …
3. [Docs (v0.2.1)](/docs/v0.2.1)
4. [Types](/docs/v0.2.1/types)
5. [Quickshell](/docs/v0.2.1/types/Quickshell)
6. [Intersection](/docs/v0.2.1/types/Quickshell/Intersection)
 

---

## Intersection: Intersection

`import Quickshell`

See [Region.intersection](/docs/v0.2.1/types/Quickshell/Region#intersection).

 

## Variants

* Combine

  Combine this region, leaving a union of this and the other region. (opposite of `Subtract`)
* Xor

  Create an intersection of this region and the other, leaving only
  the area not covered by both. (opposite of `Intersect`)
* Subtract

  Subtract this region, cutting this region out of the other. (opposite of `Combine`)
* Intersect

  Create an intersection of this region and the other, leaving only
  the area covered by both. (opposite of `Xor`)

* [Combine](#Combine)
* [Xor](#Xor)
* [Subtract](#Subtract)
* [Intersect](#Intersect)
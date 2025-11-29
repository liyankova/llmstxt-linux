---
source_url: "https://rust-lang.org/what/wasm"
title: "WebAssembly - Rust Programming Language"
crawl_date: "2025-11-29T16:22:30.702484Z"
selector: "main"
---

# WebAssembly - Rust Programming Language

![Gears](/static/images/gears.svg)

### Predictable performance

No unpredictable garbage collection pauses. No JIT compiler performance cliffs. Just low-level control coupled with high-level ergonomics.

![A microscope](/static/images/microscope.svg)

### Small code size

Small code size means faster page loads. Rust-generated `.wasm` doesn’t include extra bloat, like a garbage collector. Advanced optimizations and tree shaking remove dead code.

![Luggage](/static/images/luggage.svg)

### Modern amenities

A lively ecosystem of libraries to help you hit the ground running. Expressive, zero-cost abstractions. And a welcoming community to help you learn.

![WebAssembly Logo](/static/images/webassembly-logo.svg)

Learn more about the fast, safe, and open virtual machine called WebAssembly, and read its standard.

[Learn More](https://webassembly.org/)

![wasm ferris](/static/images/wasm-ferris.png)

Learn how to build, debug, profile, and deploy WebAssembly applications using Rust!

[Read The Book](https://rustwasm.github.io/docs/book)

![MDN logo](/static/images/mdn-logo.svg)

Learn more about WebAssembly on the Mozilla Developer Network.

[Check it out](https://developer.mozilla.org/en-US/docs/WebAssembly)

### Augment, don’t replace

The dream of WebAssembly is not to kill JavaScript but to work alongside of it, to help super charge processing-heavy or low-level tasks — tasks that benefit from Rust’s focus on performance.

### Works with familiar toolchains

Publish Rust WebAssembly packages to package registries like npm. Bundle and ship them with webpack, Parcel, and others. Maintain them with tools like `npm audit` and Greenkeeper.

### Seamless interop

Automatically generate binding code between Rust, WebAssembly, and JavaScript APIs. Take advantage of libraries like [`web-sys`](https://docs.rs/web-sys/latest/web_sys/) that provide pre-packaged bindings for the entire web platform.

![cloudflare logo](/static/images/user-logos/cloudflare.svg)

> We can compile Rust to WASM, and call it from Serverless functions woven into the very fabric of the Internet. That’s huge and I can’t wait to do more of it.

– Steven Pack, [Serverless Rust with Cloudflare Workers](https://blog.cloudflare.com/cloudflare-workers-as-a-serverless-rust-platform/)

> The JavaScript implementation [of the `source-map` library] has accumulated convoluted code in the name of performance, and we replaced it with idiomatic Rust. Rust does not force us to choose between clearly expressing intent and runtime performance.

– Nick Fitzgerald, [Oxidizing Source Maps with Rust and WebAssembly](https://hacks.mozilla.org/2018/01/oxidizing-source-maps-with-rust-and-webassembly/)

[![firefox](/static/images/firefox.png)](https://hacks.mozilla.org/2018/01/oxidizing-source-maps-with-rust-and-webassembly/)

![dropbox](/static/images/dropbox.svg)

> [Rust’s] properties make it easy to embed the DivANS codec in a webpage with WASM, as shown above.

– Daniel Reiter Horn and Jongmin Baek, [Building Better Compression Together with DivANS](https://blogs.dropbox.com/tech/2018/06/building-better-compression-together-with-divans/)
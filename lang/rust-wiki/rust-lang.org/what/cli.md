---
source_url: "https://rust-lang.org/what/cli"
title: "Command-line apps - Rust Programming Language"
crawl_date: "2025-11-29T16:22:27.911999Z"
selector: "main"
---

# Command-line apps - Rust Programming Language

![Shield with a checkmark](/static/images/cli-rustc-approved.svg)

### Solid and quick

Even if you’re just writing a short one-off
script, you can be confident it’s fast, easily testable, and gives
helpful output.

[Rust’s guarantees](/learn)

![box with a checkmark](/static/images/cli-packaging.svg)

### Easy distribution

Compile everything down to a single binary—no
need for your users to have a runtime or libraries installed.

[How to ship Rust code](https://rust-cli.github.io/book/tutorial/packaging.html)

![A note and a gear](/static/images/cli-configs.svg)

### Robust configuration

Handle configuration files across platforms with
ease. Rust will deal with namespaces and formats for you.

[Start configuring](https://rust-cli.github.io/book/in-depth/config-files.html)

![Help manual](/static/images/cli-man.svg)

### Manuals? done.

Generate manual pages for your app
automatically. Just package the generated files and you’re done.

[Learn how](https://rust-cli.github.io/book/in-depth/docs.html)

![Pipes](/static/images/cli-pipe.svg)

### Data in, data out

In addition to talking to humans, Rust has
great tools to help you talk to machines.

[Communicate with machines](https://rust-cli.github.io/book/in-depth/machine-communication.html)

![3 wood logs stacked on top of each other](/static/images/cli-logging.svg)

### Flexible logging

It’s easy to add logging, and even easier to
configure it to different targets and with different styles.

[Log, trace, comprehend](https://rust-cli.github.io/book/in-depth/human-communication.html)

What if the config file is missing or corrupt? What if the content of
that one environment variable is empty? These cases are easy to forget
about! But thanks to its approach to error handling and its library
design, Rust will point out these “what if” situations before you even
run your program.

[Rust’s error handling](https://doc.rust-lang.org/book/ch09-00-error-handling.html)

Rust allows you to be flexible in the way you organize your code. Start
with just a single file and, when you need more features, refactor your
application with the confidence that you aren’t breaking anything.

[Refactoring Rust](https://doc.rust-lang.org/book/ch12-03-improving-error-handling-and-modularity.html)

Writing a command-line app is a great way to learn Rust.

### Define your inputs

```
use clap::Parser;

/// Read some lines of a file
#[derive(Debug, Parser)]
struct Cli {
    /// Input file to read
    file: String,
    /// Number of lines to read
    #[structopt(short = 'n')]
    num: usize,
}
```

### Write your tool

```
use std::{error::Error, fs::read_to_string};

fn main() -> Result<(), Box> {
    let args = Cli::parse();
    read_to_string(&args.file)?
        .lines()
        .take(args.num)
        .for_each(|line| println!("{}", line));
    Ok(())
}
```

[Learn more with the CLI book](https://rust-cli.github.io/book/index.html)

![sentry logo](/static/images/sentry-logo-black.svg)

> One of the reasons we liked Rust was the crates.io ecosystem. [...]
> There is a lot of really good already existing infrastructure for
> building very nice command-line interfaces.

– Armin Ronacher,
[Rust at Sentry – PolyConf 2017](https://www.youtube.com/watch?v=2Xu6EdEBa5E)

---

> I have zero regrets with living in this code base. […] This was sort of
> an added bonus for me: Using Rust to make CLI or console based tools. It
> is very good at compiling for different target systems.

– Fletcher Nichol,
[Taking Rust to Production – RustFest Kyiv](https://www.youtube.com/watch?v=zAXbPnfTJg4)

![Habitat logo](/static/images/habitat.svg)
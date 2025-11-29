---
source_url: "https://rust-lang.org/what/networking"
title: "Networking - Rust Programming Language"
crawl_date: "2025-11-29T16:22:33.390585Z"
selector: "main"
---

# Networking - Rust Programming Language

![A feather](/static/images/feather.svg)

### Low footprint

Take control over resource usage to keep memory and CPU footprint to a minimum.
Get help from the compiler to make sure you’ve got it right.
And do this with an ecosystem that is productive and pleasant to use.

![A shield](/static/images/secure-shield.svg)

### Secure and reliable

Rust’s powerful type checker prevents whole classes of bugs.
Make sure you know exactly when and where state is shared and mutated.
Get help catching points of failure — before deployment.

![Connected gears](/static/images/gears-network.svg)

### Concurrent at scale

Use any mixture of concurrency approaches that works for you.
Rust will make sure you don’t accidentally share state between threads or tasks.
It empowers you to squeeze every last bit of scaling, fearlessly.

Rust has a growing ecosystem of easy-to-use libraries for the web. Here are just two examples:

### POST some JSON

```
// This will POST a body of
//     `{"lang": "rust", "body": "json"}`
#[derive(Serialize)]
struct Body<'a> {
    lang: &'a str,
    body: &'a str,
}

let client = reqwest::Client::new();
let res = client.post("http://httpbin.org/post")
    .json(&Body {
        lang: "rust",
        body: "json",
    })
    .send()?;
```

[Learn more about reqwest](https://docs.rs/reqwest/)

### Handle a JSON POST

```
#[derive(Deserialize)]
struct Task { name: String, completed: bool }

#[post("/", data = "<task>")]
fn new(task: Json<Task>) -> Flash<Redirect> {
    if task.name.is_empty() {
        Flash::error(Redirect::to("/"),
            "Cannot be empty.")
    } else {
        Flash::success(Redirect::to("/"),
            "Task added.")
    }
}
```

[Learn more about Rocket](https://rocket.rs/)

![firefox](/static/images/firefox.png)

> Migrating our Push connection infrastructure to Rust has provided us with an easier to maintain
> code-base with a focus on correctness while delivering fantastic performance. We are now
> handling up to 20 million websocket connections at once during peak hours with Rust servers.

– Benjamin Bangert, Staff Engineer, Mozilla

> Rust is foundational to the Linkerd project’s technology roadmap. Its type system allows us to
> build modular, testable, composable units without sacrificing runtime performance. What’s been
> most surprising, though, is how Rust’s lifetime/borrow checking system allows us to avoid large
> classes of resource leaks. After 2 years, I really can’t imagine using any other language for
> the job.

– Oliver Gould, CTO, [Buoyant](https://buoyant.io/)

![buoyant](/static/images/buoyant.svg)
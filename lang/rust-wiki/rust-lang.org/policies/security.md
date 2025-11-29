---
source_url: "https://rust-lang.org/policies/security"
title: "Security policy - Rust Programming Language"
crawl_date: "2025-11-29T16:22:19.435674Z"
selector: "main"
---

# Security policy - Rust Programming Language

[email security@rust-lang.org](mailto:security@rust-lang.org)

Safety is one of the core principles of Rust, and to that end, we would like to ensure that Rust has a secure implementation. Thank you for taking the time to responsibly disclose any issues you find.

All security bugs in the Rust distribution should be reported by email to [security@rust-lang.org](mailto:security@rust-lang.org). This list is delivered to a small security team. Your email will be acknowledged within 24 hours, and you’ll receive a more detailed response to your email within 48 hours indicating the next steps in handling your report.

This email address receives a large amount of spam, so be sure to use a descriptive subject line to avoid having your report be missed. After the initial reply to your report, the security team will endeavor to keep you informed of the progress being made towards a fix and full announcement. As recommended by [RFPolicy](https://en.wikipedia.org/wiki/RFPolicy), these updates will be sent at least every five days. In reality, this is more likely to be every 24-48 hours.

If you have not received a reply to your email within 48 hours, or have not heard from the security team for the past five days, there are a few steps you can take (in order):

* Contact both the security coordinators directly:
  + [Josh Stone](mailto:cuviper@gmail.com)
  + [Pietro Albini](mailto:pietro@pietroalbini.org)
* Post on the [internals forums](https://internals.rust-lang.org/)

Please note that the discussion forums are public areas. When escalating in these venues, please do not discuss your issue. Simply say that you’re trying to get a hold of someone from the security team.

[email security@rust-lang.org](mailto:security@rust-lang.org)

The Rust Security Response WG handles vulnerability reports for everything maintained and published by the Rust Project:

* The following GitHub organizations, and all repositories and CI pipelines hosted in them:
  + [`rust-lang`](https://github.com/rust-lang)
  + [`rust-lang-ci`](https://github.com/rust-lang-ci)
  + [`rust-lang-nursery`](https://github.com/rust-lang-nursery)
  + [`rust-analyzer`](https://github.com/rust-analyzer)
* The following domain names, all their subdomains, and all applications hosted within:
  + [rust-lang.org](http://rust-lang.org) (see exceptions below)
  + [rustup.rs](http://rustup.rs)
  + [crates.io](http://crates.io) (see exceptions below)
  + [docs.rs](http://docs.rs)
  + [rfcbot.rs](http://rfcbot.rs)
* All crates owned by [@rust-lang-owner](https://crates.io/users/rust-lang-owner) on [crates.io](http://crates.io).
* All extensions in the Visual Studio Marketplace published by [`rust-lang`](https://marketplace.visualstudio.com/publishers/rust-lang).
* All extensions in the Open VSX registry published by [`rust-lang`](https://open-vsx.org/namespace/rust-lang).

The following things are **outside our scope**:

* The [internals.rust-lang.org](http://internals.rust-lang.org) and [users.rust-lang.org](http://users.rust-lang.org) domains. Please follow [Discourse's Security Policy](https://github.com/discourse/discourse/blob/main/docs/SECURITY.md) for it.
* Third-party packages published on [crates.io](http://crates.io). Please follow [crates.io's Security Policy](https://crates.io/security) for them.

When reporting vulnerabilities, keep in mind that:

* Unless otherwise noted, all components of the Rust toolchain (rustc, Cargo, rust-analyzer, or any other tool shipped through rustup) assume that the user's source code and dependencies are fully trusted, reviewed and contain no malicious code. We do not consider attacks caused by compiling or analyzing malicious projects or dependencies a security vulnerability.
* Soundness issues in the Rust compiler or language are not automatically classified as a security vulnerability, but will be analyzed on a case-by-case basis if reported.
* The `regex` crate [provides guarantees about untrusted patterns](https://docs.rs/regex/latest/regex/#untrusted-input). We consider denial of service with untrusted patterns a security vulnerability only if the time spent inside of the `regex` crate is not linear, and none of the [limit methods in `RegexBuilder`](https://docs.rs/regex/latest/regex/struct.RegexBuilder.html) are able to prevent the attack.

If you have doubts on whether something falls within our scope, [please reach out](mailto:security@rust-lang.org) and we will provide guidance.

The Rust project has a 5 step disclosure process.

1. The security report is received and is assigned a primary handler. This person will coordinate the fix and release process.
2. The problem is confirmed, the affected versions are identified, and relevant domain experts from relevant Rust teams are involved.
3. Code is audited to find any potential similar problems.
4. Fixes are prepared for all supported release branches, and a CVE number is reserved. These fixes are not committed to the public repository but rather held in private repositories pending the announcement. These fixes are reviewed privately using the same review process of public changes.
5. On the embargo date, a copy of the announcement is sent to the  [Rust security mailing list](https://groups.google.com/forum/#!forum/rustlang-security-announcements) and posted on the Rust blog. The changes are pushed to the public repository and the release process is started. Within an hour, full details are published in the CVE database

This process can take some time, especially when coordination is required with maintainers of other projects. Every effort will be made to handle the bug in as timely a manner as possible, however it’s important that we follow the release process above to ensure that the disclosure is handled in a consistent manner.

The best way to receive all the security announcements is to subscribe to the [Rust security announcements mailing list](https://groups.google.com/group/rustlang-security-announcements/subscribe) (alternatively by sending an email to [rustlang-security-announcements+subscribe@googlegroups.com](mailto:rustlang-security-announcements+subscribe@googlegroups.com)). The mailing list is very low traffic, and it receives the public notifications the moment the embargo is lifted. Announcements on the mailing list are signed with the [Rust's security key](/static/keys/rust-security-team-key.gpg.ascii).

The Rust project only provides support and security updates for the most recent stable release and the latest releases in our [beta and nightly channels](https://doc.rust-lang.org/book/appendix-07-nightly-rust.html). As Rust releases must be built in the public, we will begin the release process as soon as the embargo lifts, and a release blog post will be published once updated binaries are available for download.

When a vulnerability affects software distributions, we will announce vulnerabilities 72 hours before the embargo is lifted to [distros@openwall](https://oss-security.openwall.org/wiki/mailing-lists/distros), so that distributions can update their packages when the embargo lifts.
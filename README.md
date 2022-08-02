<!-- This file is also loaded by https://peter-kehl.github.io/embedded_low_level_rust. See that presentation to view any source code included below. (That included source code doesn't show up as a part of https://github.com/ranging-rs/with_heap/blob/main/README.md.)
     Any comments starting with "presentation-" are anchors/delimiters for the above presentation.
-->
# Summary
Rust macros for ergonomic conditional compilation of `no_std`, `no_std_heap` and `std` [features](https://doc.rust-lang.org/nightly/cargo/reference/features.html).

These macros are _not_, and cannot be, configurable. The above three feature names had to be hard-coded.

# Conditional compilation and features

Basic conditional feature-based compilation is easy. It can be as simple as using 

Why are `no_std` and `std` are mutually exclusive?

# Hard 

---
<!-- The following comments hides this section from being shown by https://peter-kehl.github.io/embedded_low_level_rust. >
<!-- .slide: data-visibility="hidden" -->
See [https://peter-kehl.github.io/embedded_low_level_rust](embedded_low_level_rust) for building and testing `no_std/no_std_heap/std`.
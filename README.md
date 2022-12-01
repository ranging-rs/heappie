<!-- The following comments hides this section from being shown by
     https://peter-kehl.github.io/embedded_low_level_rust.
-->
<!-- .slide: data-visibility="hidden" -->
See also
[https://peter-kehl.github.io/embedded_low_level_rust](embedded_low_level_rust)
for building and testing `no_std/no_std_heap/std` libraries on desktop. That
also shows any source code included below.
---

<!-- That included source code doesn't show up as a part of
     https://github.com/ranging-rs/heappie/blob/main/README.md.)

     Any comments in source starting with "presentation-" are anchors/delimiters for the above presentation.
-->
# heappie - summary

Rust macros for ergonomic conditional compilation based on `no_std`,
`no_std_heap` and `std`
[features](https://doc.rust-lang.org/nightly/cargo/reference/features.html).

The feature names used/referred-to by these macros are _not_, and _cannot be_,
configurable. The above three feature names had to be hard-coded. (Explanation
of those features is later in this document.)

# Conditional compilation and features

TODO include Cargo.toml

Basic conditional feature-based compilation is easy. It can be as simple as
using:

TODO EXAMPLE

But if you depend on compound conditions, it gets repetitive. It clutters the
code. Hence suggest using macros.

_New to Rust?_ Any identifier following by an exclamation mark `!` indicates a
macro invocation. (Another type of macros, called attribute macros, start with a
hash `#`.)

TODO EXAMPLE

# Features and no_std

 * any heap-less `no_std` library will work for any purpose: `no_std` without
   heap, with heap or `std`
* but some `no_std` libraries may have both heap-less and heap parts. For
  example: extra functions or `enum` variants that work with
  `alloc::boxed::Box`, `alloc::vec::Vec`, `alloc::string::String`...
* We could have heap functions defined in separate traits in a separate (heap)
  library, but that makes types complicated. And we can't add variants to an
  existing `enum` from another crate.
* If you provide functionality for both heap and heap-less, have a
  [feature](https://doc.rust-lang.org/nightly/cargo/reference/features.html)
  called `no_std_heap` (or similar). Then conditionally compile such
  functionality (see later in this document).
---

# Why are `no_std` and `std` mutually exclusive?
* "Controversial," but proactive & clear
  * If your library can provide extra functionality in `std`, (like using
    `HashMap`)
    * have a feature for that (called, for example, `std`)
    * have a feature for `no_std`, too
    * Make those two features mutually exclusive (by a compile-time check). That
      _is_ against the [cargo book's general
      recommendation](https://doc.rust-lang.org/nightly/cargo/reference/features.html#mutually-exclusive-features),
      but they do mention this option.
    * require maximum one of those two features to be used
    * this makes any consumer crate explicit about whether they require `std` or
      `no_std`
    * benefits
      * any conflicts between dependencies (one using `std` but another using
        `no_std` of the same crate) are reported clearly
      * it simplifies troubleshooting of consumer crates and also of your
        library
      * it allows to differentiate (a small set of) consumer mid/higher level
        libraries that are `std/no_std`-agnostic. They import an
        `std/no_std`-aware library, but the `std`/`no_std` choice is left for
        the higher consumer. Such a consumer library would use the `std/no_std`
        aware library through abstractions that are `std/no_std`-independent.
        This differentiation is _not_ possible under the [cargo book's general
        recommendation](https://doc.rust-lang.org/nightly/cargo/reference/features.html#mutually-exclusive-features).
        See `slicing_any_std_test` later in this document.
    * of course, all `no_std` functionality is available under `std` feature,
      too
    * `no_std_heap` extends functionality of `no_std`. You could make
      `no_std_heap` imply `no_std` and be usable even without `no_std`, but then
      your documentation and compile checks (`no_std_heap` vs `std`) would get
      complicated. Instead, may I suggest to have `no_std_heap` require
      `no_std`. Then the exclusion checks are between `no_std` and `std` only.

If your `no_std_heap` or `std` code needs extra dependencies, use
[Features](https://doc.rust-lang.org/nightly/cargo/reference/features.html) >
[Optional
dependencies](https://doc.rust-lang.org/nightly/cargo/reference/features.html#optional-dependencies).

TODO ranging -> slicing example

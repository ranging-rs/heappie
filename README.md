<!-- This file is also loaded by https://peter-kehl.github.io/embedded_low_level_rust. See that presentation to view any source code included below. (That included source code doesn't show up as a part of https://github.com/ranging-rs/with_heap/blob/main/README.md.)
     Any comments starting with "presentation-" are anchors/delimiters for the above presentation.
-->
# Summary
Rust macros for ergonomic conditional compilation of `no_std`, `no_std_heap` and `std` [features](https://doc.rust-lang.org/nightly/cargo/reference/features.html).

# Conditional compilation and features

Basic conditional feature-based compilation is easy. It can be as simple as using 

These macros are _not_, and cannot be, configurable. The above three feature names are, and have to be, hard-coded.

<script type="text/javascript">
    document.writeln("location.href: " +location.href);
</script>
See [https://peter-kehl.github.io/embedded_low_level_rust](embedded_low_level_rust) for why `no_std` and `std` are mutually exclusive, and other reasoning.
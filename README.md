# Learning the Rust Programming Language

## Code examples

* Parser

## Documentations

* Code Guidelines:
   * https://developers.diem.com/main/docs/coding-guidelines
   * Rust Style Guide https://github.com/rust-dev-tools/fmt-rfcs/blob/master/guide/guide.md), 
   * API Guidelines https://rust-lang.github.io/api-guidelines/about.html

* Rust documentations: 
   * [X] https://foundation.rust-lang.org/
   * Learn about Rust in https://www.rust-lang.org/learn 
   * [X] The book https://doc.rust-lang.org/book/index.html 
   * Learn by examples https://doc.rust-lang.org/rust-by-example/index.html 
   * [X] Rustlings code: https://github.com/rust-lang/rustlings/ .
      It is a requirement to install msvc C++ tools from https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16

* Rust libraries and applications:
   * https://lib.rs/
 
* Rust installation:
    * [X] Rust programm: https://rustup.rs/
    * [X] IDE Eclipse: https://github.com/eclipse/corrosion or from the official eclipse installer.

* The Cargo book: Cargo is the Rust package manager. Cargo downloads your Rust package's dependencies, compiles your packages, makes distributable packages, and uploads them to crates.io, the Rust community’s package registry (this last part can be avoided).
   * https://doc.rust-lang.org/cargo/index.html 

* Antlr for rust:
   * [X] https://crates.io/crates/antlr-rust 
 
   Steps to use:
    * [X] Download the last release from github's repository https://github.com/rrevenantt/antlr4rust
    * [X] Store the grammar file
    * [X] Generate the parser java -jar <path to ANTLR4 tool> -Dlanguage=Rust MyGrammar.g4

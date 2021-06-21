# Learning the Rust Programming Language

## Code examples

* Parser

## Documentations

* Code Guidelines:
   * https://developers.diem.com/main/docs/coding-guidelines
   * Rust Style Guide https://github.com/rust-dev-tools/fmt-rfcs/blob/master/guide/guide.md), 
   * API Guidelines https://rust-lang.github.io/api-guidelines/about.html

* Rust documentations: 
   * https://foundation.rust-lang.org/
   * Learn about Rust in https://www.rust-lang.org/learn 
   * The book https://doc.rust-lang.org/book/index.html 
   * Learn by examples https://doc.rust-lang.org/rust-by-example/index.html 
   * Rustlings code: https://github.com/rust-lang/rustlings/ .

* Rust libraries and applications:
   * https://lib.rs/
 
* Rust installation in Eclipse: 
   * https://github.com/eclipse/corrosion

* The Cargo book: Cargo is the Rust package manager. Cargo downloads your Rust package's dependencies, compiles your packages, makes distributable packages, and uploads them to crates.io, the Rust community’s package registry (this last part can be avoided).
   * https://doc.rust-lang.org/cargo/index.html 

* Antlr for rust:
   * https://crates.io/crates/antlr-rust 
 
   Steps to use:
    * Download the last release from github's repository https://github.com/rrevenantt/antlr4rust
    * Store the grammar file
    * Generate the parser java -jar <path to ANTLR4 tool> -Dlanguage=Rust MyGrammar.g4

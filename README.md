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
   * [X] Cheat Sheets: https://cheats.rs/, https://programming-idioms.org/cheatsheet/Rust
    
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

## Cheets

* Compile with no warnings:  alias test='RUSTFLAGS=-Awarnings cargo +nightly test -- --nocapture'

## Utils

* translate Java to Rust: https://github.com/aschoerk/converter-page

## Compare to C in embedded systems

| features | Rust      | C |
| -- | --------  | -------- |
safety |  compile-time  | hard |
learn | similar to C  |  |
sintax | similar to C  |  |
abstractions | more | fewer |
primitive standard library | more and can be turned off | fewer |
sintax | similar to C  |  |
bitwise operation over register values [1](https://opensource.com/article/20/1/c-vs-rust-abstractions) | easy and secure to implement | complex to implement |
coding standards for programming critical systems | data      | data |
easy to verify and catch bugs | data      | data |
tools to debug | data      | data |
tools to testing | data      | data |
tools to code verification | data      | data |
integration with [LLVM](https://llvm.org/) | good | good |

GCC | not yet implemented | a bit faster |

cargo-bloat : Find out what takes most of the space in your executable
cargo-tree :  Display a tree visualization of a dependency graph

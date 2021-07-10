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
    * [X] Overview about the state of Rust support by text editors and their integrated: https://areweideyet.com/

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
* https://play.rust-lang.org/

## Compare to C in embedded systems

| features | Rust      | C |
| -- | --------  | -------- |
memory safety |  compile-time  | hard |
learn | easier  |  |
sintax | similar to C but better  |  |
abstractions | more | fewer |
primitive standard library | more and can be turned off | fewer |
sintax | similar to C  |  |
cost heap allocations | less  | high |
functions optimized for their type | X  |  |
thread-safety of all code | X  |  |
guarantess freedom from data races and memory unsafety | X  |  |
makes developers write optimal code | X  |  |
better documentation | X  |  |
bitwise operation over register values [1](https://opensource.com/article/20/1/c-vs-rust-abstractions) | easy and secure to implement | complex to implement |
coding standards for programming critical systems | There is nothing, but there are some [resources](https://github.com/rust-embedded/awesome-embedded-rust)  | X |
easy to verify and catch bugs | at compile-time | hard |
tools to debug | quite hard and [less app](https://lib.rs/development-tools/debugging), dbg, log, rust-gdb | X |
tools to testing |  [pretty_assertions](https://crates.io/crates/pretty-assertions), [others](https://lib.rs/development-tools/testing) | X |
tools to code verification |     | X |
tools to profiling | [applications](https://lib.rs/development-tools/profiling)  | X |
integration with [LLVM](https://llvm.org/) | good | good |
GCC | not yet implemented | a bit faster |


* Rust is best to learn for server side, systems, and backend developers.
* Ownership system: for example, gpio pins are move only struct. To change the functionality from input to output, you give the input pin, and returns the output pin. This way, you can break everything by changing an already used pin.
* High level: you have all the modern feature of rust: modules, iterators, generics... For example, thanks to trait, there is one code to drive a ssd1303 oled display over I2C on Linux and bare metal arm.
* Enum: so powerful to model states.
* Cargo: want a stack based vector? Just heapless ="0.3" on your Cargo.toml
* Borrow checker: no more stack dangling pointer stored on your global variable.
* Easy to use toolchain: you need rustup to build your firmware and... nothing more.

### Helper Applications

* cargo-bloat : Find out what takes most of the space in your executable
* cargo-tree :  Display a tree visualization of a dependency graph

### Resources 

* https://github.com/rust-embedded/wg : Embedded development with Rust
* https://github.com/rust-embedded/awesome-embedded-rust : List of resources related to embedded and low-level programming in the programming language Rust, including a list of useful crates.
* https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/gcc-rust.html : Benchmarks of C vs Rust
* https://benchmarksgame-team.pages.debian.net/benchmarksgame/measurements/rust.html : Benchmarks of Rust programms

### Create containing both lib.rs and main.rs

The easiest way to create a crate which contains a binary and library (such as your curl and libcurl example) is to create a folder src/bin in your project and place your a file that will serve as the entry point to your binary there (must contain a fn main() {}). In your example this would be src/bin/curl.rs.

All of your "library" code would go in src/lib.rs (and additional modules).

Finally, you'd add a section to your Cargo.toml describing where to find the binary.

    [[bin]]
    name = "curl"

So the project layout would look like this (assuming we named the project curl-rs with cargo):

    $ tree curl-rs
    curl-rs
    ├── bin
    │   └── curl.rs
    ├── Cargo.toml
    └── src
        └── lib.rs

    2 directories, 3 files
  
In order to use the functionality defined in our lib.rs it's the same as if using an external dep:

    // in src/bin/curl.rs
    extern crate curl;

    fn main() {
        // Do stuff
    }
  
Compiling this project will place a statically linked binary curl in target/{debug,release} as well as a libcurl.rlib which will be used if someone simply uses this project as a dep from something like crates.io.

### Create Modules

* https://www.tutorialspoint.com/rust/rust_modules.htm#:~:text=A%20logical%20group%20of%20code%20is%20called%20a,executable%20project%20that%20has%20a%20main%20%28%29%20method.

We can create a module in two ways:

1. In a rust file: 

        pub mod ddl3{
          pub mod ddl3visitor{}
        }

  Meaning that we have a module ddl3 that inside use another module ddl3visitor.
  
2. In a rust file:
    
        pub mod pddl3;
  
   Then in a file pddl3.rs add the content of the module:
   
        pub mod ddl3visitor;
    
   Then, in a folder ddl3/ create the file pddl3visitor.rs with the content of the module.

The two options can be combined.

### Create Objects 

* https://medium.com/analytics-vidhya/rust-adventures-from-java-class-to-rust-struct-1d63b66890cf
* https://stevedonovan.github.io/rust-gentle-intro/object-orientation.html

### Debug 

 * // println!("{:?}", parserResult);
 * dbg!(parserResult);

#### Debugging Project from VScode

  * Install extension the **CodeLLDB** (A native debugger extension for VS Code).
  * Open src/main.rs and place breakpoint to left of the line number 3 println!(“Hello, world!”)and press F5 or Run -> Start Debugging to start the debugger.
  * VS Code will display a message stating Cannot start debugging because no launch configuration has been provided. Select default options in order to generate a launch file.

### To build a project and create binary from VSCode

In the command line, execute:

    ❯ cargo build
      Finished dev [unoptimized + debuginfo] target(s) in 0.02s
    To execute the binary

    ❯ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.00s
    Running `target/debug/hello_world`
    Hello, world! 123
    
**Using Tasks**: To run VS Code task’s feature use Command+Shift+B.

To setup tasks create .vscode/tasks.json file and populate with text below providing build and run task.

    {
      "version": "2.0.0",
      "tasks": [{
       "label": "cargo build",
       "type": "shell",
       "command": "cargo build",
       "args": [],
       "group": {
         "kind": "build",
         "isDefault": true
       }
      },
      {
          "label": "cargo run",
          "type": "shell",
          "command": "cargo",
          "args": [
            "run"
            // "--release",
            // "--",
            // "arg1"
          ],
          "group": {
            "kind": "build",
            "isDefault": true
          }
         }]
    }

### Return null

You cannot return null in Rust, because there is no such concept in the language. Instead you should use Option<T>:

    fn find_parent(&self, id: &mut String) -> Option<&NodeValue> {
        if self.id == *id {
            println!("{},{}", self.id, id);
            return Some(self);
        }

        //This loop is pointless, I've kept it because it's in your original code
        for child in &self.children {
            println!("{:?}", child);
            return child.find_parent(id);
        }

        None
    }

  ### How to access value in RefCell properly
  
  https://stackoverflow.com/questions/25297447/how-to-access-value-in-refcell-properly

  ### References and lifetimes
  
  * https://blog.thoughtram.io/references-in-rust/
  * https://blog.thoughtram.io/lifetimes-in-rust/

### HashMap with general object
  
  https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=9892be55bae325096a652a97f2581c02
  
### Read an environment variable
  
      use std::env;
      ..

      fn main() {
          let silent = env::var("PV_SILENT").unwrap_or(String::new()).len() > 0;
          dbg!(silent);

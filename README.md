# Learning the Rust Programming Language

## Table of Contents  
  - [Documentations](#documentations)
  - [Installation](#installation)
  - [Useful cargo commands](#useful-cargo-commands)
  - [Compare to C in embedded systems](#compare-to-c-in-embedded-systems)
    - [Benchmarks](#benchmarks)
    - [More Resources](#more-resources)
  - [Coding](#coding)
    - [Managing versions X.Y.Z](#versions-xyz)
    - [Utils](#utils)
    - [Libraries](#libraries)
  - [Additional knowledge](#additional-knowledge)
    - [Continous programming](#continous-programming)
    - [Create containing both lib.rs and main.rs](#create-containing-both-librs-and-mainrs)
    - [Create Modules](#create-modules)
    - [Create Objects](#create-objects)
    - [Data structures](#data-structures)
      - [HashSet example](#hashset-example)
      - [HashMap with general object](#hashmap-with-general-object)
      - [LinkedHashMap example](#linkedhashmap-example)
    - [Debug](#debug)
      - [Debugging Project from VScode](#debugging-project-from-vscode)
    - [To build a project and create binary from VSCode](#to-build-a-project-and-create-binary-from-vscode)
    - [Return null](#return-null)
    - [Enables mutation inside an immutable struct.](#enables-mutation-inside-an-immutable-struct)
    - [How to access value in RefCell properly](#how-to-access-value-in-refcell-properly)
    - [References and lifetimes](#references-and-lifetimes)
    - [Read an environment variable](#read-an-environment-variable)
    - [Read arguments from command line](#read-arguments-from-command-line)
    - [Trait example](#trait-example)
    - [Cast beteween two Traits](#cast-beteween-two-traits)
    - [Traits in function arguments and trait bounds](#traits-in-function-arguments-and-trait-bounds)
    - [Returning traits](#returning-traits)
    - [Trait combos](#trait-combos)
    - [Associated Types](#associated-types)
    - [Share code between multiple Cargo projects](#share-code-between-multiple-cargo-projects)
    - [Patterns](#patterns)
    - [Docker file example](#docker-file-example)
    - [Create GUI](#create-gui)
    - [Draw macro](#draw-macro)

## Documentations

Code / API Guidelines:
   * [X] [Rust API Guidelines](https://rust-lang.github.io/api-guidelines/about.html)
   * [X] [API documentation conventions](https://rust-lang.github.io/rfcs/1574-more-api-documentation-conventions.html#appendix-a-full-conventions-text)
   * [X] [Making useful documentation comments](https://doc.rust-lang.org/book/ch14-02-publishing-to-crates-io.html#making-useful-documentation-comments)
   * [ ] [Rust Style Guide](https://github.com/rust-dev-tools/fmt-rfcs/blob/master/guide/guide.md), 

Rust documentations: 
   * [X] [The book](https://doc.rust-lang.org/book/index.html)
   * [X] Cheat Sheets: [Cheats](https://cheats.rs/), [Programming Idioms](https://programming-idioms.org/cheatsheet/Rust)
   * [X] [Learn by examples](https://doc.rust-lang.org/rust-by-example/index.html)
   * [ ] [Rust Lang Foundation](https://foundation.rust-lang.org/)
   * [ ] [Learn about Rust](https://www.rust-lang.org/learn)
   * [ ] [Rustlings code](https://github.com/rust-lang/rustlings/)
      It is a requirement to install [msvc C++ tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)

[The Cargo book](https://doc.rust-lang.org/cargo/index.html): Cargo is the Rust package manager. Cargo downloads your Rust package's dependencies, compiles your packages, makes distributable packages, and uploads them to crates.io, the Rust community’s package registry (this last part can be avoided).
   
## Installation

  * [X] [Rust programm](https://rustup.rs/)
  * [IDEs](https://www.rust-lang.org/tools):
    * [X] [Overview of Rust's IDE](https://areweideyet.com/): overview about the state of Rust support by text editors.
    * [X] [IntelliJ IDEA](https://plugins.jetbrains.com/plugin/8182-rust/docs/rust-quick-start.html): The best one to work is IntelliJ IDEA with the Rust pluging. 
    * [ ] [IDE Eclipse](https://github.com/eclipse/corrosion): Version of Eclipse that support Rust. It can also be installed from the official eclipse installer.

## Useful cargo commands

* **cargo fmt**: Format automatically the code.
   
* **cargo +nightly clippy**: Improve code. 
   
* **cargo +nightly doc --no-deps --open --document-private-items**: Generate doc. 

        --no-deps : by default cargo generate the documentation of all the dependencies
        --open : one finish open it in the browser
          
* **alias test='RUSTFLAGS=-Awarnings cargo +nightly test -- --nocapture'**: Compile with no warnings.
* **cargo-bloat**: Find out what takes most of the space in your executable.
* **cargo-tree**: Display a tree visualization of a dependency graph.

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
tools to debug | quite hard and [less app](https://lib.rs/development-tools/debugging), [dbg](https://www.youtube.com/watch?v=bWH-nL7v5F4) with plugings [pwndbg] (https://github.com/pwndbg/pwndbg). [Gdb on Windows](https://rpg.hamsterrepublic.com/ohrrpgce/GDB_on_Windows), log, rust-gdb | X |
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

### Benchmarks

* Benchmarks of C vs Rust: https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/gcc-rust.html 
* Benchmarks of Rust programms: https://benchmarksgame-team.pages.debian.net/benchmarksgame/measurements/rust.html 

### More Resources 

* Embedded development with Rust: https://github.com/rust-embedded/wg
* List of resources related to embedded and low-level programming in the programming language Rust, including a list of useful crates: https://github.com/rust-embedded/awesome-embedded-rust 

## Coding

### Managing versions X.Y.Z

We should specify the versions of a Cargo package as X.Y.Z, where:

* X is Major change 
* Y is Minor change
* Z is Patch 

In Rust, the values X.Y.Z changes as follows:

if X < 1 then 
  * 0 : Major 
  * Y : Minor = Breaking changes
  * Z : Patch = Whatever

if X >= 1 then 
  * X : Major = Breaking change
  * Y : Minor = Add functionality
  * Z : Patch = Bug fixes

### Utils

* [Play Rust](https://play.rust-lang.org/)
* [Translate Java to Rust](https://github.com/cguz/java-to-rust)

### Libraries

* Find rust libraries and applications:
   * [X] [Lib](https://lib.rs/)

* Antlr for rust:
   * [X] https://crates.io/crates/antlr-rust 
 
   Steps to use:
    * [X] Download the last release from github's repository https://github.com/rrevenantt/antlr4rust
    * [X] Store the grammar file
    * [X] Generate the parser java -jar <path to ANTLR4 tool> -Dlanguage=Rust MyGrammar.g4
  

## Additional knowledge

### Mutability

* https://manishearth.github.io/blog/2015/05/17/the-problem-with-shared-mutability/

### Continous programming

* Check the code before do commit: 
  * vim .git/hook/pre-commit
      
        cargo fmt
        exec cargo clippy -- -D warnings
        
   * chmod a+x .git/hook/pre-commit

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

**Additional binaries:** We can create additional binaries in the folder bin:

     curl-rs
        ├── bin
        │   └── curl.rs
        │   └── curl2.rs
        │   └── curl3.rs
        ├── Cargo.toml
        └── src
            └── lib.rs

If we do this, we need to specify which binary to run on the command line when you do your cargo run command:

    $ cargo run --bin curl2
    $ cargo run --bin curl3

### Create Modules

* https://www.tutorialspoint.com/rust/rust_modules.htm#:~:text=A%20logical%20group%20of%20code%20is%20called%20a,executable%20project%20that%20has%20a%20main%20%28%29%20method.

We can create a module in two ways:

1. In a rust file: 

        pub mod ddl3{
          pub mod ddl3visitor{}
        }

  Meaning that we have a module ddl3 that inside use a sub module ddl3visitor.
  
2. In a rust file:
    
        pub mod pddl3;
  
   Then in a file pddl3.rs add the content of the module:
   
        pub mod ddl3visitor;
    
   Then, in a folder (module) ddl3/ create the file (submodule) pddl3visitor.rs with the content of the module.

The two options can be combined.

### Create Objects 

* https://medium.com/analytics-vidhya/rust-adventures-from-java-class-to-rust-struct-1d63b66890cf
* https://stevedonovan.github.io/rust-gentle-intro/object-orientation.html

## Data structures
  
### HashMap with general object
  
  https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=9892be55bae325096a652a97f2581c02
  
### LinkedHashMap example
  
  * https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=21b4722c25dff6d28fcdf48e4c4e4166
  * https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=15f2cea99e1c8228091a98b49a9b4996
  
### HashSet example
  
  https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=38f25460e3423a189437c2aa3ba0bd20
  
## Debug 

 * // println!("{:?}", parserResult);
 * dbg!(parserResult);

### Debugging Project from VScode

  * Install extension the **CodeLLDB** (A native debugger extension for VS Code).
  * Open src/main.rs and place breakpoint to left of the line number 3 println!(“Hello, world!”)and press F5 or Run -> Start Debugging to start the debugger.
  * VS Code will display a message stating Cannot start debugging because no launch configuration has been provided. Select default options in order to generate a launch file.

## To build a project and create binary from VSCode

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

## Return null

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

## Enables mutation inside an immutable struct.
  
We can do it with Cell<T>, which enables mutation inside an immutable struct. 
  
In other words, it enables “interior mutability”. Example took from https://doc.rust-lang.org/std/cell/struct.Cell.html

    use std::cell::Cell;

    struct SomeStruct {
        regular_field: u8,
        special_field: Cell<u8>,
    }

    let my_struct = SomeStruct {
        regular_field: 0,
        special_field: Cell::new(1),
    };

    let new_value = 100;

    // ERROR: `my_struct` is immutable
    // my_struct.regular_field = new_value;

    // WORKS: although `my_struct` is immutable, `special_field` is a `Cell`,
    // which can always be mutated
    my_struct.special_field.set(new_value);
    assert_eq!(my_struct.special_field.get(), new_value);
  
Other structure is CellRef : A mutable memory location with dynamically checked borrow rules.

If you ever want the threaded versions, Arc replaces Rc and Mutex or RwLock replaces Cell/RefCel.
  
## How to access value in RefCell properly
  
  https://stackoverflow.com/questions/25297447/how-to-access-value-in-refcell-properly

## References and lifetimes
  
  * https://blog.thoughtram.io/references-in-rust/
  * https://blog.thoughtram.io/lifetimes-in-rust/
 
## Read an environment variable
  
    use std::env;
    ..

    fn main() {
        let silent = env::var("PV_SILENT").unwrap_or(String::new()).len() > 0;
        dbg!(silent);
  
## Read arguments from command line
  
    use clap::{App, Arg};

    fn main() {
        let matches = App::new("pipeviewer")
            .arg(Arg::with_name("infile")).help("Read from a file")
            .arg(
                Arg::with_name("outfile")
                    .short("o")
                    .long("outfile")
                    .takes_value(true)
                    .help("Write output to a file instead of stdout")
            )
            .arg(Arg::with_name("silent")
                .short("s")
                .long("silent"))
            .get_matches();

        let infile = matches.value_of("infile").unwrap_or_default();
    }
  
  In Cargo.toml add:
  
    [dependencies]
    clap = "3.0.0-beta.2"
  
## Trait example
  
  * [OOP Java](https://medium.com/analytics-vidhya/rust-adventures-from-java-class-to-rust-struct-1d63b66890cf)
  * [Element as a trait, others as Instance](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=636db8a49ac2c266450e8f6ac335b839
  * [Element as Instance, other as traits](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=cd6a6a5accdd4ab06ac46bc90e3ef4dc)
  * [Element as Instance, other as traits. With Enum](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=afb01a39b3641afd665f410d1c7e497f).
  
## Cast beteween two Traits. 
  
  Source from: https://stackoverflow.com/questions/34419561/can-i-cast-between-two-traits
  
  No, it is not possible. Some solutions are:
  
  * If you own these traits, then you can add **as_foo** to the **Bar** trait and vice versa. [playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=8b92e55d587228bb55e70ddcab6a7cb5)
  * You could create an enum that holds either a **Box\<dyn Foo>** or a **Box\<dyn Bar>** and then pattern match. 
  * You could move the body of **bar** into the body of **foo** for that implementation.
  * You could implement a third trait **Quux** where calling **\<FooStruct as Quux>::quux** calls **Foo::foo** and calling **\<BarStruct as Quux>::quux** calls **Bar::foo** followed by **Bar::bar**.
    
## Traits in function arguments and trait bounds
  
Consider these two functions:

      use std::fmt::Debug;

      fn f(a: &Debug, b: &Debug) {
          todo!()
      }

      fn g<T: Debug>(a: &T, b: &T) {
          todo!()
      }
  
Ignoring the fact that they don’t do anything, the function f will accept any two arguments that implement the Debug trait, even if they are two different types. On the other hand, g will only accept two arguments of the same type, but that type can be any type that implements Debug.
  
## Returning traits

We can use traits as return types from functions. There are two different ways to do this: impl Trait and Box<dyn Trait>. Again, the differences are subtle but important.

      use std::fmt::Debug;

      fn dyn_trait(n: u8) -> Box<dyn Debug> {
          todo!()
      }

      fn impl_trait(n: u8) -> impl Debug {
          todo!()
      }
  
The dyn_trait function can return any number of types that implement the Debug trait and can even return a different type depending on the input argument. This is known as a trait object. “The Rust Programming Language” book has a section on using trait objects for dynamic dispatch if you want to delve further.

The impl_trait method, on the other hand, can only return a single type that implements the Debug trait. In other words, the function will always return the same type.

While this difference may make impl Trait appear less useful than trait objects, it has a very important feature (in addition to being easier to type and to work with): you can use it to return iterators and closures. This is explained further in the book’s chapter on traits, “Returning Types that Implement Traits.”
  
## Trait combos
  
T: Trait1 + Trait2 + Trait3.

Source: https://blog.logrocket.com/rust-traits-a-deep-dive/ 
  
## Associated Types
  
    trait Associated {
        type T;
        fn get(&self) -> Self::T;
    }
  
Source: https://blog.thomasheartman.com/posts/on-generics-and-associated-types

## Share code between multiple Cargo projects
  
The way to do this is to make a library:

cargo new --lib my_library
Instead of a src/main.rs, this will have a src/lib.rs as its “root” module. Any types/functions/submodules in this root module that are marked pub will be usable from within other Cargo projects. For example:

    // my_library/src/lib.rs
    pub fn do_stuff() {
       println!("Hi");
    }
  
To use this code from one of your binary projects like my_project, you can put the following in my_project/Cargo.toml:

    [dependencies]
    my_library = { path = "../my_library" }

(The path value can be either an absolute path or a relative path to the my_library directory.)

Now, everywhere within my_project, you can access public items from the my_library crate, just like you can from other libraries:

    // my_project/src/main.rs
    fn main() {
        my_library::do_stuff();
    }

## Patterns
  
* [Enum wrapper for traits](https://play.rust-lang.org/?version=stable&mode=debug&edition=2018&gist=2f40c19dfcdec7978fd7c716639b1388). Source https://bennetthardwick.com/dont-use-boxed-trait-objects-for-struct-internals
  
## Docker file example
  
  https://github.com/integer32llc/rust-playground/blob/master/compiler/base/Dockerfile
  
## Create GUI 
  
  https://github.com/iced-rs/iced

## Draw macro
  
  https://lukaslueg.github.io/macro_railroad_wasm_demo/
  
## Implement Self-referential types
  
  https://users.rust-lang.org/t/how-can-we-teach-people-about-self-referential-types/65362

## Test macros
  
  https://eli.thegreenplace.net/2021/testing-multiple-implementations-of-a-trait-in-rust/
  
## Examples youtube
  
  https://www.youtube.com/watch?v=b4mS5UPHh20
  
  https://cxx.rs/
  
 Safe and unsafe: https://doc.rust-lang.org/nomicon/meet-safe-and-unsafe.html
  
  https://rust-unofficial.github.io/too-many-lists/
  
 Cargo https://github.com/facebookincubator/cargo-guppy
  
  Discord: https://discord.com/invite/aVESxV8
  
  Rust has opened me to a new way of thinking when it comes to designing code - being able to find a bug, and then change the code so that similar bugs become errors at compile time is mind blowing—as discussed in depth https://fasterthanli.me/articles/abstracting-away-correctness and https://fasterthanli.me/articles/aiming-for-correctness-with-types.

---
layout: post
title: Rust learning
tags: [Learn, Courses, Rust]
description: "Rust learning"
---

# Rust programming

## Hello world !

```rust
fn main() {
    println!("Hello, world!");
}
```

fn means function, the main function is the beginning of every Rust program.

**println!()** prints text to the console and its **!** indicates that it’s a macro rather than a function.

Rust files should have **.rs** file extension.

## println!()

```
fn main() {
    println!("{}, {}!", "Hello", "world");
    println!("{0}, {1}!", "Hello", "world");
    println!("{greeting}, {name}!", greeting="Hello", name="world");

    println!("{:?}", [1,2,3]); // [1, 2, 3]
    println!("{:#?}", [1,2,3]);
    /*
        [
            1,
            2,
            3
        ]
    */

    // The format! macro is used to store the formatted string.
    let x = format!("{}, {}!", "Hello", "world");
    println!("{}", x); // Hello, world!

    // Rust has a print!() macro as well
    print!("Hello, world!"); // Without new line
    println!(); // A new line

    print!("Hello, world!\n"); // With new line
}
```

## Cargo

### Create a project

A crate is a package, which can be shared via [crates.io](https://crates.io/). A crate can produce an executable or a library. In other words, it can be a **binary** crate or a **library** crate.

```
# Binary
cargo new <BINARY_NAME> --bin

# Library
cargo new <LIBRARY_NAME> --lib
```

- **Cargo.toml**(capital c) is the configuration file which contains all of the metadata that Cargo needs to compile your project.
- **src** folder is the place to store the source code.
- Each crate has an implicit crate root/ entry point. **main.rs** is the crate root for a binary crate and **lib.rs** is the crate root for a library crate.

### Build a project

```
cargo build
```

### Run a project

```
cargo run
```

### Check a project

Cargo also provides a command called `cargo check`. This command quickly checks your code to make sure it compiles but doesn’t produce an executable:

```
cargo check
```

Why would you not want an executable? Often, `cargo check` is much faster than `cargo build`, because it skips the step of producing an executable. If you’re continually checking your work while writing the code, using `cargo check` will speed up the process!

### Building for release

When your project is finally ready for release, you can use :

```
cargo build --release
```

To compile it with optimizations, this command will create an executable in *target/release* instead of *target/debug*. The optimizations make your Rust code run faster, but turning them on lengthens the time it takes for your program to compile. This is why there are two different profiles: one for development, when you want to rebuild quickly and often, and another for building the final program you’ll give to a user that won’t be rebuilt repeatedly and that will run as fast as possible.

## Variables

### Binding

The first thing to know in Rust is that all variables are constant by default. To declare a mutable variable, use the keyword mut.

```
let a; // Declaration; without data type
a = 5; // Assignment

let b: i8; // Declaration; with data type 
b = 5;

let t = true;        // Declaration + assignment; without data type
let f: bool = false; // Declaration + assignment; with data type

let (x, y) = (1, 2); // x = 1 and y = 2

let mut z = 5;
z = 6;

let z = { x + y }; // z = 3
```

### Constant

```
const MAX_HEALTH: i32 = 100;
```

### Shadowing

Sometimes, while dealing with data, initially we get them in one unit but need to transform them into another unit for further processing. In this situation, instead of using different variable names, Rust allows us to **redeclare the same variable with a different data type and/ or with a different mutability setting**. We call this Shadowing.

```
fn main() {
    let x: f64 = -20.48; // float
    let x: i64 = x.floor() as i64; // int
    println!("{}", x); // -21

    let s: &str = "hello"; // &str
    let s: String = s.to_uppercase(); // String
    println!("{}", s) // HELLO
}
```

### Increment

```
let mut i = 0;
i += 1
```

### Unused variable

If we start the name of a variable with a '_', we won't get a compiler warning if it is unused.

```
let _i = 0;
```

## Functions


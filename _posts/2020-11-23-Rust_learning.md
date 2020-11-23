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

```rust
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

```rust
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

```rust
const MAX_HEALTH: i32 = 100;
```

### Shadowing

Sometimes, while dealing with data, initially we get them in one unit but need to transform them into another unit for further processing. In this situation, instead of using different variable names, Rust allows us to **redeclare the same variable with a different data type and/ or with a different mutability setting**. We call this Shadowing.

```rust
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

```rust
let mut i = 0;
i += 1
```

### Unused variable

If we start the name of a variable with a '_', we won't get a compiler warning if it is unused.

```rust
let _i = 0;
```

## Functions

- Named functions are declared with the keyword **`fn`**
- When using **arguments**, you **must declare the data types**.
- By default, functions **return an empty [tuple](https://learning-rust.github.io/docs/a8.primitive_data_types.html#tuples)/ `()`**. If you want to return a value, the **return type must be specified** after **`->`**

### Passing arguments

```rust
fn print_sum(a: i8, b: i8) {
    println!("sum is: {}", a + b);
}
```

### Returning values

```rust
fn plus_one(a: i32) -> i32 {
    a + 1
}
```

There is no ending `;` in the above code, it means this is an expression which equals to `return a + 1;`.

### Closures

- Also known as **anonymous functions** or **lambda functions**.
- The **data types of arguments and returns are optional**.

```rust
fn main() {
    let x = 2;
    let square = |i| {i * i;};
    println!("{}", square(x));
}
```

## Primitive Data Types

### Bool

```rust
let x = true;
let y: bool = false;

// no TRUE, FALSE, 1, 0
```

### Char

```rust
let x = 'x';
let y: char = '😎';

// no "x", only single quotes
```

### Integer

- i8
- i16
- i32
- i64
- i128

```rust
let x = 10; // The default integer type in Rust is i32
let y: i8 = -128;
```

 You can use **`min_value()`** and **`max_value()`** functions to find min and max of each integer type.

```rust
i8::min_value();
```

### Unsigned integer

- u8
- u16
- u32
- u64
- u128

```Rust
let x: u32 = 2500;
```

 You can use **`min_value()`** and **`max_value()`** functions to find min and max of each integer type.

```rust
i8::min_value();
```

### Float

```rust
let x = 1.5; // The default float type in Rust is f64
let y: f64 = 2.0;
```

 Should avoid using `f32`, unless you need to reduce memory consumption badly or if you are doing low-level optimization, when  targeted hardware does not support for double-precision or when single-precision is faster than double-precision on it.

### Array

Fixed size list of elements of same data type. Arrays are **immutable** by default and **even with `mut`, its element count cannot be changed**. If you are looking for a dynamic/growable array, you can use [vectors](https://learning-rust.github.io/docs/b1.vectors.html). Vectors can contain any type of elements but all elements must be in the same data type.

```rust
let a = [1, 2, 3];
let a: [i32; 3] = [1, 2, 3]; // [Type; NO of elements]

let b: [i32; 0] = []; // An empty array

let mut c: [i32; 3] = [1, 2, 3];
c[0] = 2;
c[1] = 4;
c[2] = 6;

println!("{:?}", c); // [2, 4, 6]
println!("{:#?}", c);
//  [
//      2,
//      4,
//      6,
//  ]

let d = [0; 5];   // [0, 0, 0, 0, 0]
let e = ["x"; 5]; // ["x", "x", "x", "x", "x"]
```

### Tuple

Fixed size ordered list of elements of different (or same) data types. Tuples are also **immutable** by default and **even with `mut`, its element count cannot be changed. Also, if you want to change an  element’s value, the new value should have the same data type of  previous value**.

```rust
let a = (1, 1.5, true, 'a');
let a: (i32, f64, bool, char) = (1, 1.5, true, 'a');

let mut b = (1, 1.5);
b.0 = 2;
b.1 = 3.0;

println!("{:?}", b); // (2, 3.0)
println!("{:#?}", b);
// (
//   2,
//   3.0,
// )

let (c, d) = b; // c = 2, d = 3.0
let (e, _, _, f) = a; // e = 1, f = 'a'

let g = (0,); // single-element tuple
let h = (b, (2, 4), 5); // ((2, 3.0), (2, 4), 5)
```

### Slice

Dynamically-sized reference to another data structure. Imagine you want to get/ pass a part of an array or any other data  structure. Instead of copying it to another array (or same data  structure), Rust allows for creating a view/ reference to access only  that part of the data. This view/ reference can be mutable or immutable.

```rust
let a: [i32; 4] = [1, 2, 3, 4]; // Parent Array

let b: &[i32] = &a; // Slicing whole array
let c = &a[0..4]; // From 0th position to 4th(excluding)
let d = &a[..]; // Slicing whole array

let e = &a[1..3]; // [2, 3]
let f = &a[1..]; // [2, 3, 4]
let g = &a[..3]; // [1, 2, 3]
```

### Str

Unsized UTF-8 sequence of Unicode string slices. It’s an **immutable/ statically allocated slice** holding an **unknown sized sequence of UTF-8** code points stored in somewhere in memory. **`&str`** is used to borrow and assign the whole array to the given variable binding.

```rust
let a = "Hello, world."; // a: &'static str
let b: &str = "こんにちは, 世界!";
```

#### String

A [`String`](https://doc.rust-lang.org/std/string/struct.String.html) type can be generated from a `&str` type, via the **[`to_string()`](https://doc.rust-lang.org/std/string/trait.ToString.html)** or **[`String::from()`](https://doc.rust-lang.org/std/string/struct.String.html#method.from)** methods. With [**`as_str()`**](https://learning-rust.github.io/docs/a8.primitive_data_types.html) method, a `String` type can be converted to a `&str` type.

```rust
let s: &str = "Hello"; // &str

let s = s.to_string(); // String
let s = String::from(s); // String

let s = s.as_str(); // &str
```

#### String concatenation

```rust
let (s1, s2) = ("some", "thing"); // both &str
// All bellow codes return `String`; something

let s = String::from(s1) + s2; // String + &str

let mut s = String::from(s1); // String
s.push_str(s2); // + &str

let s = format!("{}{}", s1, s2); // &str/String + &str/String

let s = [s1, s2].concat(); // &str or String array
```

## Control Flows

### if - else if - else

```rust
let age = 13;

if age < 18 {
    println!("Hello, child !");
} else if a > 18 {
	println!("Hello, adult !"); 
} else {
	println!("Hello, god ?");
}
```

### Match

Rust provides pattern matching via the `match` keyword, which can be used like a C `switch`.

```rust
let tshirt_width = 20;
let tshirt_size = match tshirt_width {
    16 => "S", // check 16
    17 | 18 => "M", // check 17 and 18
    19 ..= 21 => "L", // check from 19 to 21 (19,20,21)
    22 => "XL",
    _ => "Not Available",
};

println!("{}", tshirt_size); // L
```

### Loop

```rust
let mut a = 0;

loop {
    if a == 0 {
        println!("Skip Value : {}", a);
        a += 1;
        continue;
    } else if a == 2 {
        println!("Break At : {}", a);
        break;
    }

    println!("Current Value : {}", a);
    a += 1;
}
```

### While

```rust
let mut b = 0;

while b < 5 {
    if b == 0 {
        println!("Skip value : {}", b);
        b += 1;
        continue;
    } else if b == 2 {
        println!("Break At : {}", b);
        break;
    }

    println!("Current value : {}", b);
    b += 1;
}
```

### For

```rust
for b in 0..6 {
  if b == 0 {
    println!("Skip Value : {}", b);
    continue;
  } else if b == 2 {
    println!("Break At : {}", b);
    break;
  }

  println!("Current value : {}", b);
}
```

#### Array/vector

```rust
let group : [&str; 4] = ["Mark", "Larry", "Bill", "Steve"];

for person in group.iter() { // group.iter() turn the array into a simple iterator
  println!("Current Person : {}", person);
}
```


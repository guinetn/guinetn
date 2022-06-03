---
title: "About rust lang"
date: 2022-06-03T19:07:13+01:00
draft: false
---
# Rust

Open-source language; 6000 contributors. MIT and Apache License 

- https://doc.rust-lang.org
- https://play.rust-lang.org

```rs
fn main() { 				
    println!("Hello!");
}
```
>rustc main.rs    // create main.exe
>main.exe

Creating projects:
>cargo new hello
  structure created: /src/main.rs /.toml (dependencies), /.gitignore
>cargo run
>cargo run build


Focuses to be safe, secure, concurrent with combination of 
- Static typing: prevent errors at compile time
  compiler is very strict: reliable and have fewer bugs
  it catches a lot of errors that would normally go unnoticed: no never used variable possible
- Dynamic typing: flexibility and easier refactoring
- Ownership and borrowing: ensure that data is accessed safely and efficiently
- Modern syntax and design, a mixture of assembler and a functional programming language, and it looks very strange to the uninitiated.
- Like C++, it supports low-level code, high performance, and direct memory access.
- Rust doesn't have classes: use custom data types (structs..) to represent types of objects
- Rust code uses snake case for function and variable names
  all letters are lowercase and underscores separate words
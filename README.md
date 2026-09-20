# Rune

> An experimental programming language built from scratch in Rust.

Rune is a small programming language created to explore how programming languages work internally, from lexical analysis and parsing to runtime execution, scopes, functions, control flow, and type checking.

Rune currently uses a **tree-walk interpreter** and is under active development.

> [!WARNING]
> Rune is experimental software.
>
> Syntax, semantics, diagnostics, runtime behavior, and internal architecture may change during the `0.x` development cycle.

---

## Table of Contents

- [About Rune](#about-rune)
- [Current Features](#current-features)
- [Quick Start](#quick-start)
- [File Extension](#file-extension)
- [Language Syntax](#language-syntax)
  - [Statements](#statements)
  - [Variables](#variables)
  - [Types](#types)
  - [Strings](#strings)
  - [Characters](#characters)
  - [Numbers](#numbers)
  - [Booleans](#booleans)
  - [Arithmetic](#arithmetic)
  - [Comparisons](#comparisons)
  - [Logical Operators](#logical-operators)
  - [Operator Precedence](#operator-precedence)
  - [Blocks and Scopes](#blocks-and-scopes)
  - [If / Else](#if--else)
  - [While](#while)
  - [For](#for)
  - [Break](#break)
  - [Continue](#continue)
  - [Functions](#functions)
  - [Parameters](#parameters)
  - [Return](#return)
  - [Print](#print)
  - [Println](#println)
  - [Input](#input)
- [Complete Example](#complete-example)
- [How Rune Works](#how-rune-works)
- [Project Structure](#project-structure)
- [Building](#building)
- [Running Rune Programs](#running-rune-programs)
- [Error Handling](#error-handling)
- [What Rune Does Not Support Yet](#what-rune-does-not-support-yet)
- [Roadmap](#roadmap)
- [Versioning](#versioning)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

# About Rune

Rune is an experimental programming language implemented in Rust.

The project is built as a hands-on exploration of programming language implementation. Instead of relying entirely on an existing language runtime, Rune implements its own core pipeline:

```text
Rune source
    │
    ▼
  Lexer
    │
    ▼
 Tokens
    │
    ▼
 Parser
    │
    ▼
  AST
    │
    ▼
Interpreter
    │
    ▼
 Output
```

The current implementation includes:

- lexical analysis;
- tokenization;
- parsing;
- abstract syntax trees;
- expressions;
- variables;
- mutability;
- explicit types;
- type inference;
- lexical scopes;
- conditionals;
- loops;
- functions;
- function calls;
- return values;
- built-in functions;
- terminal input and output.

---

# Current Features

## Core language

- `.rune` source files
- Semicolon-terminated statements
- Identifiers
- String literals
- Character literals
- Integer literals
- Floating-point literals
- Boolean literals
- Parenthesized expressions
- Variable declarations
- Mutable and immutable variables
- Variable reassignment
- Explicit types
- Type inference
- Nested lexical scopes
- Variable shadowing

## Variables

- `let`
- `var`
- assignment with `=`

## Types

Rune currently recognizes:

```text
i8
i16
i32
i64

u8
u16
u32
u64

f16
f32
f64

string
char
bool
void
```

## Arithmetic operators

```text
+
-
*
/
%
```

## Comparison operators

```text
==
!=
<
<=
>
>=
```

## Logical operators

```text
!
&&
||
```

## Control flow

- `if`
- `else if`
- `else`
- `while`
- `for`
- `break`
- `continue`

## Functions

- Function declarations
- Typed parameters
- Function calls
- Optional return type
- `void` functions
- `return`
- Recursion

## Input and output

- `print(...)`
- `println(...)`
- `io.input()`
- `io.input("Prompt: ")`

## Runtime

- Nested scope stack
- Variable lookup across scopes
- Mutable variable lookup
- Runtime type validation
- Integer range checking
- Numeric coercion where supported
- Short-circuit logical evaluation
- User-defined functions
- Built-in functions

---

# Quick Start

Create a file named:

```text
hello.rune
```

Add:

```rune
let name: string = io.input("What is your name? ");

print("Hello, ");
println(name);
```

Run it:

```bash
cargo run -- hello.rune
```

Example:

```text
What is your name? Mateus
Hello, Mateus
```

---

# File Extension

Rune source files use:

```text
.rune
```

Examples:

```text
main.rune
hello.rune
calculator.rune
game.rune
test.rune
```

---

# Language Syntax

## Statements

Most simple statements end with a semicolon:

```rune
let name = "Rune";
println(name);
```

Block-based constructs do not require a semicolon after the closing brace:

```rune
if true {
    println("Hello");
}
```

---

# Variables

Rune supports both immutable and mutable variables.

## `let`

`let` creates an immutable variable:

```rune
let name = "Rune";
let version = 0.4;
```

An immutable variable cannot be reassigned:

```rune
let value = 10;

// Runtime error:
value = 20;
```

## `var`

`var` creates a mutable variable:

```rune
var counter = 0;

counter = counter + 1;

println(counter);
```

Output:

```text
1
```

## Explicit types

```rune
let age: i32 = 13;
let price: f64 = 19.99;
let language: string = "Rune";
let active: bool = true;
```

## Type inference

When no type annotation is provided, Rune infers the variable type from its value:

```rune
let number = 42;
let decimal = 3.14;
let message = "Hello";
let enabled = true;
```

---

# Types

Rune currently supports several built-in types.

## Signed integers

```text
i8
i16
i32
i64
```

Example:

```rune
let value: i32 = 42;
```

## Unsigned integers

```text
u8
u16
u32
u64
```

Example:

```rune
let count: u32 = 100;
```

## Floating-point values

```text
f16
f32
f64
```

Example:

```rune
let pi: f64 = 3.14;
```

## String

```rune
let language: string = "Rune";
```

## Character

```rune
let letter: char = 'R';
```

## Boolean

```rune
let enabled: bool = true;
```

## Void

`void` is used as a function return type when no value is returned.

A function without an explicit return type is treated as `void`.

```rune
function greet(name: string) {
    println(name);
}
```

---

# Strings

Strings are enclosed in double quotes:

```rune
let message = "Hello, world!";
```

Strings can be printed directly:

```rune
println("Rune");
```

Rune also supports string concatenation with `+`:

```rune
let first = "Rune";
let second = " language";

let result = first + second;

println(result);
```

---

# Characters

Character literals use single quotes:

```rune
let letter: char = 'R';

println(letter);
```

---

# Numbers

## Integers

```rune
let a = 10;
let b: i32 = 20;
```

## Floating-point numbers

```rune
let price = 19.99;
let version: f64 = 0.4;
```

Rune validates explicitly typed integers against their allowed ranges.

For example, assigning a value outside the valid range of `i8` results in an error.

---

# Booleans

Rune supports:

```rune
true
false
```

Example:

```rune
let enabled: bool = true;

println(enabled);
```

---

# Arithmetic

Rune supports:

| Operator | Meaning |
|---|---|
| `+` | Addition |
| `-` | Subtraction |
| `*` | Multiplication |
| `/` | Division |
| `%` | Modulo |

Examples:

```rune
let addition = 10 + 5;
let subtraction = 10 - 5;
let multiplication = 10 * 5;
let division = 10 / 5;
let remainder = 10 % 3;

println(addition);
println(subtraction);
println(multiplication);
println(division);
println(remainder);
```

---

# Comparisons

Rune supports:

```text
==
!=
<
<=
>
>=
```

Examples:

```rune
println(10 == 10);
println(10 != 5);
println(5 < 10);
println(5 <= 5);
println(10 > 5);
println(10 >= 10);
```

---

# Logical Operators

Rune supports boolean logic.

## NOT

```rune
let active = true;

println(!active);
```

## AND

```rune
let logged_in = true;
let verified = true;

if logged_in && verified {
    println("Access granted");
}
```

## OR

```rune
let admin = false;
let moderator = true;

if admin || moderator {
    println("Access granted");
}
```

Rune uses short-circuit evaluation for `&&` and `||`.

---

# Operator Precedence

Rune respects operator precedence.

Example:

```rune
let result = 2 + 3 * 4;

println(result);
```

Output:

```text
14
```

Grouping changes the order:

```rune
let result = (2 + 3) * 4;

println(result);
```

Output:

```text
20
```

A simplified precedence order is:

```text
lowest

||
&&
== !=
< <= > >=
+ -
* / %
!
function calls / member access
primary expressions

highest
```

---

# Blocks and Scopes

Blocks use braces:

```rune
{
    let value = 10;
    println(value);
}
```

Variables declared inside a block are not accessible after the block ends:

```rune
{
    let secret = 42;
}

// Error: secret no longer exists here.
println(secret);
```

Inner scopes can access variables from outer scopes:

```rune
let value = 10;

{
    println(value);
}
```

## Shadowing

Rune supports variable shadowing across different scopes:

```rune
let value = 10;

{
    let value = 20;
    println(value);
}

println(value);
```

Output:

```text
20
10
```

---

# If / Else

Basic conditional:

```rune
let age: i32 = 13;

if age >= 13 {
    println("Allowed");
} else {
    println("Not allowed");
}
```

Rune also supports `else if`:

```rune
let temperature: i32 = 28;

if temperature >= 30 {
    println("Hot");
} else if temperature >= 20 {
    println("Warm");
} else {
    println("Cold");
}
```

Conditions must evaluate to a boolean.

---

# While

```rune
var counter: i32 = 0;

while counter < 5 {
    println(counter);

    counter = counter + 1;
}
```

Output:

```text
0
1
2
3
4
```

---

# For

Rune supports C-style `for` loops:

```rune
for var i: i32 = 0; i < 5; i = i + 1 {
    println(i);
}
```

The initializer must currently be a variable declaration and the increment must be an assignment.

---

# Break

`break` exits the nearest loop:

```rune
var i: i32 = 0;

while true {
    if i == 5 {
        break;
    }

    println(i);
    i = i + 1;
}
```

---

# Continue

`continue` skips the rest of the current loop iteration:

```rune
for var i: i32 = 0; i < 10; i = i + 1 {
    if i % 2 != 0 {
        continue;
    }

    println(i);
}
```

---

# Functions

Functions are declared using the `function` keyword.

```rune
function add(a: i32, b: i32): i32 {
    return a + b;
}
```

Call the function:

```rune
let result = add(10, 20);

println(result);
```

Output:

```text
30
```

---

# Parameters

Function parameters require explicit types:

```rune
function greet(name: string) {
    print("Hello, ");
    println(name);
}

greet("Rune");
```

Multiple parameters are separated by commas:

```rune
function multiply(a: i32, b: i32): i32 {
    return a * b;
}

println(multiply(6, 7));
```

---

# Return

Functions can return values:

```rune
function square(value: i32): i32 {
    return value * value;
}

println(square(5));
```

Output:

```text
25
```

Void functions can use an empty return:

```rune
function greet() {
    println("Hello");
    return;
}
```

---

# Recursion

Rune functions can call themselves:

```rune
function factorial(n: i32): i32 {
    if n <= 1 {
        return 1;
    }

    return n * factorial(n - 1);
}

println(factorial(5));
```

Output:

```text
120
```

---

# Print

`print(...)` writes output without automatically adding a newline.

```rune
print("Hello, ");
print("world!");
```

Output:

```text
Hello, world!
```

Multiple arguments are supported:

```rune
let name = "Rune";

print("Language:", name);
```

---

# Println

`println(...)` writes output followed by a newline.

```rune
println("Hello, world!");
```

Multiple arguments are also supported:

```rune
let language = "Rune";
let version = 0.4;

println("Language:", language);
println("Version:", version);
```

---

# Input

Rune provides terminal input through the built-in `io` namespace.

## With a prompt

```rune
let name: string = io.input("What is your name? ");

print("Hello, ");
println(name);
```

Example:

```text
What is your name? Mateus
Hello, Mateus
```

## Without a prompt

```rune
print("Type something: ");

let text: string = io.input();

println(text);
```

`io.input()` reads one line from standard input and returns it as a `string`.

Currently supported forms:

```rune
io.input();
```

and:

```rune
io.input("Prompt: ");
```

The function accepts **zero or one argument**.

When provided, the argument must be a string.

Invalid:

```rune
io.input(123);
```

Invalid:

```rune
io.input("A", "B");
```

---

# Complete Example

This example combines many of Rune's current features:

```rune
let language: string = "Rune";

println("=== Rune Demo ===");

let name: string = io.input("Name: ");
let age_text: string = io.input("Age as text: ");

print("Hello, ");
println(name);

var counter: i32 = 0;

while counter < 3 {
    println("Counter:", counter);
    counter = counter + 1;
}

function is_even(number: i32): bool {
    return number % 2 == 0;
}

function factorial(number: i32): i32 {
    if number <= 1 {
        return 1;
    }

    return number * factorial(number - 1);
}

for var i: i32 = 0; i < 10; i = i + 1 {
    if i == 8 {
        break;
    }

    if !is_even(i) {
        continue;
    }

    println("Even:", i);
}

{
    let scoped_value: i32 = 42;

    println("Scoped value:", scoped_value);
}

println("5! =", factorial(5));

println("Language:", language);
println("Age input:", age_text);

println("=== End ===");
```

---

# How Rune Works

Rune currently uses a tree-walk interpreter.

```text
.rune source
     │
     ▼
   Lexer
     │
     ▼
   Tokens
     │
     ▼
   Parser
     │
     ▼
    AST
     │
     ▼
 Interpreter
     │
     ▼
   Result
```

## Lexer

The lexer converts source characters into tokens.

Example:

```rune
let result: i32 = 2 + 3;
```

Conceptually:

```text
Let
Identifier("result")
Colon
Identifier("i32")
Equal
IntegerLiteral(2)
Plus
IntegerLiteral(3)
Semicolon
EOF
```

## Parser

The parser converts tokens into structured syntax.

It handles:

- variable declarations;
- assignments;
- blocks;
- conditionals;
- loops;
- function declarations;
- returns;
- expressions;
- function calls;
- member access;
- operator precedence.

## AST

The AST represents the structure of the program.

Example:

```rune
2 + 3 * 4
```

Conceptually:

```text
        Add
       /   \
      2    Multiply
          /        \
         3          4
```

A member call such as:

```rune
io.input("Name: ")
```

is represented conceptually as:

```text
Call
├── callee
│   └── Member
│       ├── object: Identifier("io")
│       └── name: "input"
└── arguments
    └── StringLiteral("Name: ")
```

## Interpreter

The interpreter:

- evaluates expressions;
- manages nested scopes;
- stores variables;
- validates types;
- resolves functions;
- executes control flow;
- executes built-in functions;
- reads terminal input;
- produces output.

---

# Project Structure

A simplified project layout:

```text
rune/
├── Cargo.toml
├── README.md
└── src/
    ├── main.rs
    ├── token/
    ├── lexer/
    ├── ast/
    ├── parser/
    └── interpreter/
```

## `token`

Defines token kinds used by the lexer and parser.

## `lexer`

Responsible for:

- scanning characters;
- recognizing keywords;
- reading identifiers;
- reading strings;
- reading characters;
- reading numbers;
- operators;
- punctuation;
- source position tracking.

## `ast`

Defines:

- expressions;
- statements;
- operators;
- function parameters;
- Rune types;
- program structure.

## `parser`

Responsible for:

- statement parsing;
- expression parsing;
- operator precedence;
- member access;
- function calls;
- variable declarations;
- assignments;
- blocks;
- conditions;
- loops;
- functions;
- returns.

## `interpreter`

Responsible for:

- evaluating expressions;
- executing statements;
- scopes;
- variables;
- mutability;
- type validation;
- built-ins;
- functions;
- loops;
- control flow;
- terminal input/output.

## `main.rs`

Acts as the CLI entry point.

---

# Building

Rune is written in Rust.

Check that Rust is installed:

```bash
rustc --version
cargo --version
```

Clone the repository:

```bash
git clone https://github.com/MateusSoaresL/rune.git
cd rune
```

Build:

```bash
cargo build
```

Optimized build:

```bash
cargo build --release
```

The release executable is normally generated under:

```text
target/release/
```

---

# Running Rune Programs

Create:

```text
main.rune
```

Example:

```rune
let name: string = io.input("Name: ");

println("Hello,", name);
```

Run:

```bash
cargo run -- main.rune
```

Or after a release build:

```bash
./target/release/rune main.rune
```

On Windows:

```text
rune.exe
```

---

# Error Handling

Rune reports syntax and runtime errors with source location information where available.

Examples may include:

```text
Expected expression at 4:10
```

```text
Undefined identifier 'value' at 8:5
```

```text
Cannot assign to immutable variable 'value' at 3:1
```

```text
Type mismatch: expected i32, found String(...) at 2:5
```

```text
Division by zero at 7:12
```

```text
io.input() expects 0 or 1 argument, got 2
```

```text
io.input() prompt must be a string
```

Rune also validates invalid control flow, such as:

- `break` outside a loop;
- `continue` outside a loop;
- `return` outside a function.

---

# What Rune Does Not Support Yet

Rune is still experimental.

The following features are not currently documented as supported:

## Imports and modules

```rune
import math;
```

or:

```rune
use math;
```

## Arrays

```rune
let values = [1, 2, 3];
```

## Objects

```rune
let user = {
    name: "Rune"
};
```

## Classes

```rune
class User {
}
```

## Package manager

Rune does not currently include a package manager.

## Native compilation

Rune currently executes code through a tree-walk interpreter rather than compiling Rune source directly to native machine code.

---

# Roadmap

## Implemented

- [x] `.rune` source files
- [x] Lexer
- [x] Tokens
- [x] Parser
- [x] AST
- [x] Tree-walk interpreter
- [x] String literals
- [x] Character literals
- [x] Integer literals
- [x] Floating-point literals
- [x] Boolean literals
- [x] Identifiers
- [x] `let`
- [x] `var`
- [x] Assignment
- [x] Explicit variable types
- [x] Type inference
- [x] Integer range validation
- [x] Block scopes
- [x] Variable shadowing
- [x] Arithmetic operators
- [x] Modulo
- [x] Equality operators
- [x] Comparison operators
- [x] Logical operators
- [x] Short-circuit evaluation
- [x] Operator precedence
- [x] Parenthesized expressions
- [x] `if`
- [x] `else if`
- [x] `else`
- [x] `while`
- [x] `for`
- [x] `break`
- [x] `continue`
- [x] Functions
- [x] Typed parameters
- [x] Function calls
- [x] Return types
- [x] `return`
- [x] Recursion
- [x] `print`
- [x] `println`
- [x] `io.input()`
- [x] `io.input("Prompt: ")`
- [x] Source line tracking
- [x] Source column tracking
- [x] Runtime errors

## Future possibilities

- [ ] Arrays
- [ ] Objects
- [ ] Modules
- [ ] Imports
- [ ] Standard library expansion
- [ ] String interpolation
- [ ] More built-in namespaces
- [ ] Better diagnostics
- [ ] REPL
- [ ] Formatter
- [ ] Language Server Protocol
- [ ] Package manager
- [ ] Intermediate Representation
- [ ] Bytecode
- [ ] Virtual machine
- [ ] Native compilation
- [ ] Optimization passes

---

# Future Compiler Architecture

Rune may eventually evolve from:

```text
Source
  ↓
Lexer
  ↓
Parser
  ↓
AST
  ↓
Interpreter
```

toward something like:

```text
Rune Source
     │
     ▼
   Lexer
     │
     ▼
   Parser
     │
     ▼
    AST
     │
     ▼
Semantic Analysis
     │
     ▼
Typed AST
     │
     ▼
     IR
     │
     ▼
Optimization
     │
     ▼
Code Generation
     │
     ▼
Native Code / Bytecode
```

Possible future backends may include:

```text
LLVM
Cranelift
Custom bytecode VM
Custom native backend
```

No final backend is guaranteed.

---

# Versioning

Rune follows Semantic Versioning where practical:

```text
MAJOR.MINOR.PATCH
```

During early development, Rune remains in the `0.x` series.

Example:

```text
v0.4.0
```

Breaking changes may occur between `0.x` releases.

A future `v1.0.0` should represent a substantially more stable language specification and public interface.

---

# Contributing

Bug reports, suggestions, discussions, and pull requests are welcome.

When reporting a bug, include:

1. Rune version
2. Operating system
3. Rune source code
4. Expected output
5. Actual output
6. Error message

Use the smallest reproducible example possible.

Example:

```rune
let result: i32 = (2 + 3) * 4;

println(result);
```

---

# Development Status

Rune is under active development.

Internal APIs are not considered stable.

This includes:

```text
Token definitions
AST nodes
Parser internals
Interpreter internals
Runtime values
Built-in APIs
Error formats
Module layout
```

Users should rely on documented Rune syntax rather than Rust implementation details.

---

# License

No license is assumed by this README.

Before accepting external contributions or distributing Rune for reuse, add an explicit license file.

Common choices include:

```text
MIT
Apache-2.0
MIT OR Apache-2.0
```

---

# Author

Created by **Mateus Soares**.

GitHub:

```text
https://github.com/MateusSoaresL
```

Repository:

```text
https://github.com/MateusSoaresL/rune
```

---

# Final Note

Rune is an experimental programming language being built incrementally from the lexer upward.

The current language already supports a substantial interpreted core:

```text
Variables
Types
Expressions
Scopes
Conditionals
Loops
Functions
Input / Output
```

The next stages can focus on expanding the standard library, improving diagnostics, strengthening the language model, and eventually exploring bytecode or native compilation.
# a-very-brief-intro-to-rust

<hr>

## links

- web: https://ashleygwilliams.github.io/a-very-brief-intro-to-rust/#1
- github: https://github.com/ashleygwilliams/a-very-brief-intro-to-rust

### PRs and issues welcome!

made by [@ag_dubs](https://twitter.com/ag_dubs) who is, at best, an advanced beginner in Rust

<hr>

### This guide is an intro to Rust syntax and concepts.

<hr>

## What is Rust?

Rust is a systems programming language that runs blazingly fast, prevents
segfaults, and guarantees thread safety.

<hr>

## Rust Philosophy

* Favor explicit over implicit
* Zero-cost abstractions
* Only pay for what you use
* Memory safety
* Small standard library
* Error handling
* Stability without stagnation

<hr>

## install rust

The best way to install Rust is with [rustup](https://www.rustup.rs/). rustup is a Rust
version manager. To install it type:

```
curl https://sh.rustup.rs -sSf | sh
```

To keep your rust up-to-date with the latest stable version of rust,
type:

```
rustup update
```

To check which version of Rust you have type:

```
rustc --version
```

<hr>

## What is Cargo?

* Package manager
* Build tool
* Test runner
* Documentation generator

<hr>

## setting up a project

There are many ways to setup a project in Rust, but this is the simplest.

1. Create a repository on Github
2. Clone the repository
3. `cd` into the repository directory
4. Type `cargo init .`
  * Use `--bin` if you are not writing a library

This will create several files and folders for you automatically:

- `Cargo.toml`: metadata about your project and its dependencies
- `.gitignore`: ignores compiled files built by Rust
- `src/lib.rs` or `src/main.rs`: where your Rust code goes

<hr>

## setting up a project

#### `lib.rs` vs `main.rs`

There are 2 main types of projects you can make in Rust: a library and not
a library.

If you are writing a <strong>library</strong>, it means you intend for your
code to be used in someone else's application as a crate or module.
If you want to do this, you should use a `lib.rs`.

If you are writing a <strong>not library</strong>, it means that you'd like
to write code that compiles into a binary that someone can run. If you
want to do this, you need to use a `main.rs`. Inside the `main.rs` you
should have a `main` function that looks like this:

```rust
fn main() {
  // your app code goes here
}
```

<hr>

## Files created

- `Cargo.toml`: metadata about your project and its dependencies
- `.gitignore`: ignores compiled files built by Rust
- `src/main.rs`: where your Rust code goes

<hr>

## `Cargo.toml`

```toml
[package]
name = "rustbridge"
version = "0.1.0"
authors = ["Carol (Nichols || Goulding) <carol.nichols@gmail.com>"]

[dependencies]
```

<hr>

## `src/main.rs`

```rust
fn main() {
    println!("Hello, world!");
}
```

<hr>

## Run it!

* `cargo run`
* Should print "Hello, world!"
* Now you have more files:
  * `target` directory: all the built stuff
  * `Cargo.lock`: locks your dependencies (we don't have any yet)
* Try printing out something else!
* Try printing out two things!

<hr>

## API Documentation

https://doc.rust-lang.org/
or
`rustup doc`

Click on "Standard Library API Reference"
or
`rustup doc --std`

<hr>

## Syntax + Concepts mostly the same as other languages

<hr>

## Comments

* Double slash at the beginning of a line (`//`)
* Try commenting out one of your lines printing!
* There are other kinds of comments but this is the most common

<hr>

## storing values

To get started using Rust you'll probably want to assign values so that
you can use them. To do this in Rust:

```
let name = "ashley";
let age = 30;
```

* Try making more variables and printing them all out in one `println!`

If you want to make a constant, you must specify a type:

```
const FAVENUM: u32 = 6;
```

<hr>

## Experiment

What happens if you run this:

```rust
let apples = 100;
apples += 50;
println!("I have {} apples", apples);
```

<hr>

## Mutability

Variables are *immutable* by default in Rust.

```rust
let mut apples = 100;
apples += 50;
println!("I have {} apples", apples);
```

<hr>

## types

There are a lot of types, but just to get you started:

- `u32`: unsigned 32-bit integer
- `i32`: signed 32-bit integer
- `f64`: floating point number
- `String` and/or `&str`: more on these below
- `bool`: a boolean

<hr>

## Type inference

* Every value has a type that the compiler has to know about.
* Most of the time, the compiler can figure it out.
* Sometimes it can't, and you'll get an error and need to add an annotation.
* We could have written `let age: i32 = 30;`
* A place we **must** specify types is function definitions.

???

* Types come after the name

<hr>

## Functions

```rust
fn add_fifty(n: i32) -> i32 {
    n + 50
}

fn main() {
    println!("Lots: {}", add_fifty(100));
}
```

<hr>

## Conditionals: `if`

```rust
fn main() {
    let age = 13u32;
    if n < 13 {
        println!("You may see G or PG movies");
    } else if n < 17 {
        println!("You may see G, PG, or PG-13 movies");
    } else {
        println!("You are old.");
        println!("You may see G, PG, PG-13, or R movies");
    }
}
```
???

* Shorthand for numeric type annotation
* Age can't be negative, compiler will make sure we don't have negative ages

<hr>

## Conditionals: `match`

Kinda like a switch. But better.

```rust
fn main() {
    let age = 13u32;
    match age {
        0...12 => println!("You may see G or PG movies"),
        13...16 => println!("You may see G, PG, or PG-13 movies"),
        _ => {
            println!("You are old.");
            println!("You may see G, PG, PG-13, or R movies")
        },
    }
}
```

<hr>

## Arrays

Kinda like arrays in other languages, but worse.

```rust
let mut color = [255, 0, 255];
color[0] = 100;
println!("The color is {:?}", color);
```

<hr>

## Quick but Useful Tangent #1: `println!` formatting

* `{}` is called `Display` formatting; only on primitive types by default
* `{:?}` is called `Debug` formatting; more types have this by default
* Display is for end users, Debug is for... debugging
* Rust doesn't want to make assumptions
* My favorite: `{:#?}` = pretty debug
* [`fmt` docs](https://doc.rust-lang.org/stable/std/fmt/index.html)

<hr>

## Quick but Useful Tangent #2: `panic!`

* Panic stops your program with a message.

```rust
fn main() {
    panic!("aaaaa!");
}
```

What happens in the last example if we try to access an element out of bounds of the array?

```rust
let color = [255, 0, 255];
let index = 9;
println!("The 10th element is {:?}", color[index]);
```

<hr>

## Vectors

Most of the time, you probably want a vector rather than array.

```rust
let mut prices = vec![30, 100, 2];
prices[0] = 25;
prices.push(40);
println!("All the prices are: {:?}", prices);
```
<hr>

## Looping (and ranges)

* `for` loops are most common:

```rust
for i in 0..10 {
    println!("Number {}", i);
}
```

```rust
let names = vec!["Carol", "Jake", "Marylou", "Bruce"];
for name in names.iter() {
    println!("Hi {}!", name);
}
```

* `loop` creates an infinite loop
* `while` loops run while their condition is true
* `break` exits the current loop

<hr>

## Iterators

```
for i in (0..10).filter(|x| x % 2 == 0) {
    println!("i = {}", i);
}

for i in (0..10).map(|x| x * x ) {
    println!("i = {}", i);
}

let sum = (0..10).fold(0, |acc, x| acc + x);
println!("sum = {}", sum);
```

* See the [Iterator docs](https://doc.rust-lang.org/stable/std/iter/trait.Iterator.html) for lots more fun stuff.
* The `|x| x % 2 == 0` in the examples is a closure, they can be used in other situations too.

<hr>

## Enums

* Nice to use with `match`

```rust
enum TrafficLight {
    Red,
    Yellow,
    Green,
}
let light = TrafficLight::Green;

match light {
    TrafficLight::Red => println!("STOP!"),
    TrafficLight::Yellow => println!("Slow down!"),
    TrafficLight::Green => println!("Go go go!"),
}
```

<hr>

## Enums

* Better than in other languages: can hold values!

```rust
enum GameType {
    SinglePlayer,
    MultiPlayer(u32),
}

let game = GameType::MultiPlayer(4);

match game {
    GameType::SinglePlayer => println!("How about solitaire?"),
    GameType::MultiPlayer(2) => println!("How about checkers?"),
    GameType::MultiPlayer(4) => println!("How about bridge?"),
    GameType::MultiPlayer(num) => {
        println!("How about {}-player tag?", num)
    },
}
```

<hr>

## testing

Rust has unit testing built in! You can write tests in their own file or right
inline with your code.

To designate a test write `#[test]` above a code block with asserts:

```rust
fn say_hello(name: &str) -> String {
  let who = match name {
    Some(n) => n,
    None => "World",
  };
  format!("Hello, {}!", who)
}

#[test]
fn it_should_say_hello() {
  assert_eq!(say_hello(None), String::from("Hello, World!"));
  assert_eq!(say_hello(Some("World")), String::from("Hello, World!"));
  assert_eq!(say_hello(Some("ashley")), String::from(("Hello, ashley!"));
}
```

<hr>

## Syntax + Concepts particular to Rust

<hr>

## Option

**Rust doesn't have `nil`/`null`** so to express that a value might be something or nothing, Rust has the `Option` type.

Option is an enum provided by the standard library:

```rust
enum Option<T> {
    Some(T),
    None
}
```

<hr>

## Using Option

```rust
let mut instructors = vec!["Carol"];

let a = instructors.pop();
println!("a is {:?}", a);

let b = instructors.pop();
println!("b is {:?}", b);
```

<hr>

## Using Option

```rust
let a = Some("Carol");

let name = a.expect("No name present");
println!("Name is {} bytes long", name.len());
```

<hr>

## Using Option

```rust
let b: Option<&str> = None;

match b {
    Some(name) => {
        println!("Other name is {} bytes long", name.len())
    },
    None => {
        println!("No name!")
    }
}
```

<hr>

## Result

* Another enum in the standard library
* For when something could succeed or fail
* Rust doesn't have exceptions; using `Result` is how you handle errors.

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

<hr>

## Using Result

```rust
let numstr = "6";
let num = numstr.parse::<i32>();
println!("num = {:?}", num);

let numstr = "florp";
let num = numstr.parse::<i32>();
println!("num = {:?}", num);
```

<hr>

## Using Result

```rust
let numstr = "6";
let num = numstr.parse::<i32>();
let num = num.expect("should have a number");

println!("num + 5 = {}", num + 5);
```

<hr>

## Using Result

```rust
let numstr = "florp";
let num = numstr.parse::<i32>();

let answer = match num {
    Ok(n) => n + 5,
    Err(_) => 0,
};
println!("Answer is {}", answer);
```

<hr>

## `try!` macro to propagate errors up

* Can only be used in methods/functions that return `Result`!!!!

```rust
fn add_five_to_string(s: String) ->
    Result<i32, std::num::ParseIntError> {

    let ans = try!(s.parse::<i32>()) + 5;
    Ok(ans)
}
```

<hr>

## Strings: WARNING

* Strings in Rust feel complicated
* We're sorry

???

Working with strings in Rust is more complicated than working with strings in other languages.

Strings are actually complicated in all languages, it's just that most hide the complexity from you and make choices for you. Rust makes you be explicit with the choices.

<hr>

## Two string types

### `String`

* Allocated
* Growable
* Can create with either:
  * `something.to_string()`
  * `String::from("string slice")`

### `&str`

* Pronounced "string slice"
* View into string data stored somewhere else
* Hardcoded strings are `&str`s

<hr>

## A common problem

```rust
fn fizz(num: u32) -> String {
    if num % 3 == 0 {
        "Fizz"
    } else {
        num.to_string()
    }
}
```

<hr>

## Slices

* A view into some data
* Points to the start of the view
* Knows how long the view is

<hr>

## Slice syntax

* Vector type: `Vec<i32>`
* Corresponding slice type: `&[i32]`

```rust
let v = vec![1, 2, 3, 4, 5];
let piece = &v[3..];
println!("piece of v = {:?}", piece);
```

<hr>

## String Slices

```rust
let s = String::from("Call me Ishmael blah blah...");
let part = &s[0..4];

println!("part is '{}'", part);
```

<hr>

## Ownership

* The *owner* of a resource is who is responsible for cleaning it up.
* When owners go out of scope, Rust automatically calls the cleanup code.

```rust
fn main() {
    let v = vec![1, 2, 3];
    println!("v is valid here! {:?}", v);
}
```

<hr>

## Transferring Ownership

* When you pass an argument to a function, ownership is transferred to the function.
* We say that something is *moved*.

```rust
fn main() {
    let v = vec![1, 2, 3];
    print_vec(v);
    print_vec(v);
}

fn print_vec(v: Vec<i32>) {
    println!("v is {:?}", v);
}
```

<hr>

## References

* Let you borrow a resource you don't own
* A reference is only valid as long as the owner is valid. Rust ensures you aren't using an invalid reference *at compile time*.
* Slices are a specific type of reference.

```rust
fn main() {
    let v = vec![1, 2, 3];
    print_vec(&v[..]);
    print_vec(&v[..]);
}

fn print_vec(v: &[i32]) {
    println!("v is {:?}", v);
}
```

<hr>

## Mutable References

* Like variables, references are immutable by default, but you can make them mutable with `mut`.
* You may have many immutable references in a scope
* You may only have one mutable reference and no immutable references in a scope

```rust
fn main() {
    let mut v = vec![1, 2, 3];
    change_vec(&mut v[..]);
    change_vec(&mut v[..]);
    println!("v is {:?}", v);
}

fn change_vec(v: &mut [i32]) {
    v[0] *= 5;
}
```

<hr>

## Not allowed to have mutable and immutable references in the same scope.

```rust
fn main() {
    let mut v = vec![1, 2, 3];

    let f = &v[0];
    v.clear();

    println!("What would f be? {}", f);
}
```

<hr>

## Further learning
### Syntax + Concepts we didn't cover but that are things

* Tests
* Lifetimes
* Tuples
* Structs
* Methods
* `if let`
* FFI
* Traits
* Generics
* Macros
* Threads
* Composition over inheritance

<hr>

## good resources

- The Rust Docs, https://doc.rust-lang.org/
- The Rust Book, https://doc.rust-lang.org/book/
- into_rust Screencasts, http://intorust.com/
- The Rust Play Ground, https://play.rust-lang.org/
- Rust by Example, http://rustbyexample.com/
- Rust on exercism.io, http://exercism.io/languages/rust
- New Rustacean Podcast, http://www.newrustacean.com/

<hr>

# go forth and write some Rust!

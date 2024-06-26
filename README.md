# symbolang
Simple programming language. Implementation TODO
---
# Examples
#### Hello World!
```rust
import use io; // Include println, avoid namespacing.

let main() {
    println("Hello, World!");
}
```
#### Fibonacci
```rust
let fib(n: i32) -> i32 {
    return match n {
        ..0: 0, // invalid input
        1 | 2: 1,
        else: fib(n-1) + fib(n-2)
    };
}
// ... main() etc.
```
#### Looping
```rust
import use io;

let main() {
    // For
    let x = 25;
    for i: (0..x) {
        println("{}", i);
    }
    // While
    let some_var = 10;
    for some_var > 0 {
        some_var -= 1;
    }

    // For Each
    let numbers = [10, 20, 30, 40];
    for number: numbers {
        println("Number: {}", number);
    }
}
```
#### CLI Work
```rust
import use io;

let main(args: [str]) {
    if args.len() == 1: crash("NO arguments provided!");
    for (i, arg) : args[1..].enumerate() {
        println("argument at {} = {}", i, arg);
    }
    // Input
    let user_input = readline(stdin).assert;
}
```

#### Error Handling
```rust
let may_crash(crash_and_burn: bool) -> Try<i32, str> {
    return crash_and_burn? Try::Fail("Crashed!") else Try::Ok(69420);
}

let main() {
    // Contains value Try::Ok(69420)
    let ok = may_crash(false);
    // 'Unwrap' value (will crash on error)
    let ok_2 = may_crash(false).assert;
    // Check for error value
    let ok_3 = may_crash(true).on_error(err => {
        crash("Got an error: {}", err);
    });
}
```
#### Reading a File
```rust
import use io;
import fs;

let main() {
    let file = fs.readfile("test.txt");
    match file {
        Ok(content): println("Content = {}", content),
        Fail(msg): println("ERROR: {}, msg),
    }
}
```
#### Mutating
```rust
let modify_x(x: var i32) {
    x += 1;
}
let main() {
    var x: i32 = 9;
    modify_x(var x);
}
```
#### Enumerations
```rust
import use io;
enum Direction {
    North, South, East, West
}

for Direction let {
    let print(var self) {
        let text = match self {
            .North: "North",
            .South: "South",
            .East: "East",
            .West: "West",
        };
        println("{}", text);
    }
}
```
#### Structs
```rust
struct Person {
    age: u8,
    name: str,
}

for Person let {
    let empty() -> Person {
        return Person {age: 0, name: ""};
    }
    let new(age: u8, name: str) -> Person {
        return Person {age, name};
    }
}
```

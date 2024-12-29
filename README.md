# Day 1: Understanding Rust Basics

This guide introduces foundational concepts in Rust, providing insights into key language features and practical examples to solidify your understanding.

## Associated Functions and Their Usage
Associated functions are functions tied to a type rather than an instance. They are defined in an `impl` block and accessed using `::`. For example, `String::new()` creates a new, empty `String`.

### Example:
```rust
fn main() {
    let s = String::new();
    println!("String: {}", s); // Output: String: 
}
```

Rust also allows defining custom associated functions for your types:
```rust
struct MyStruct;

impl MyStruct {
    fn new() -> Self {
        MyStruct
    }

    fn describe() {
        println!("This is MyStruct.");
    }
}

fn main() {
    let instance = MyStruct::new(); // Creates a new instance of MyStruct
    MyStruct::describe(); // Prints: This is MyStruct.
}
```

---

## Type-Level vs Instance-Level Functions
In Rust, there is a distinction between type-level and instance-level functions. Type-level functions operate on the type itself, while instance-level functions operate on specific instances.

### Comparison:
| **Feature**          | **Type-Level**                            | **Instance-Level**                     |
|----------------------|-------------------------------------------|-----------------------------------------|
| **Definition**       | Associated with the type itself          | Associated with an instance of the type|
| **Call Syntax**      | `TypeName::function_name()`              | `instance_name.method_name()`          |
| **Access to `self`** | No (`self` is not present)               | Yes (`self`, `&self`, or `&mut self`)  |
| **Example**          | `String::new()`                          | `string_instance.len()`                |

---

## Common Examples of Associated Functions
Rust provides several associated functions for its standard types:

### Vectors
```rust
fn main() {
    let mut numbers: Vec<i32> = Vec::new(); // Creates an empty vector
    numbers.push(42);
    println!("Numbers: {:?}", numbers); // Output: Numbers: [42]
}
```

### Hash Maps
```rust
use std::collections::HashMap;

fn main() {
    let mut scores: HashMap<String, i32> = HashMap::new();
    scores.insert("Alice".to_string(), 10);
    println!("Scores: {:?}", scores); // Output: Scores: {"Alice": 10}
}
```

---

## Enums: `Option` and `Result`
Rust uses enums like `Option` and `Result` to handle optional values and errors explicitly and safely.

### Option
`Option` represents a value that may or may not exist. It has two variants:
- `Option::Some(value)` for a present value.
- `Option::None` for no value.

#### Example:
```rust
fn find_value(values: &[i32], target: i32) -> Option<usize> {
    values.iter().position(|&x| x == target)
}

fn main() {
    match find_value(&[1, 2, 3], 2) {
        Some(index) => println!("Found at index: {}", index),
        None => println!("Not found"),
    }
}
```

### Result
`Result` represents the outcome of an operation that may succeed or fail. It has two variants:
- `Result::Ok(value)` for success.
- `Result::Err(error)` for failure.

#### Example:
```rust
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        Err("Cannot divide by zero".to_string())
    } else {
        Ok(a / b)
    }
}

fn main() {
    match divide(10, 2) {
        Ok(result) => println!("Result: {}", result),
        Err(err) => println!("Error: {}", err),
    }
}
```

---

## Declaring Integers and Default Values
Integers in Rust are primitive types and do not have associated functions like `String::new()`. However, you can initialize them directly or use the `Default` trait.

### Examples:
```rust
let x: i32 = 0; // Default value for i32
let y = u64::default(); // Using `Default` trait for unsigned 64-bit integer
```

You can mimic `String::new()` with:
```rust
fn main() {
    let x: i32 = i32::default(); // Default value is 0
    println!("x = {}", x); // Output: x = 0
}
```

---

## Reading Integers with `io::stdin()`
Rust's `io::stdin()` is used for reading user input. Since input is read as a string, you must parse it into the desired type, like `i32`.

### Basic Example:
```rust
use std::io;

fn main() {
    let mut input = String::new();
    println!("Enter a number:");

    io::stdin()
        .read_line(&mut input)
        .expect("Failed to read line");

    let number: i32 = input.trim().parse().expect("Invalid number");
    println!("You entered: {}", number);
}
```

### With Error Handling:
```rust
use std::io;

fn main() {
    let mut input = String::new();
    println!("Enter a number:");

    io::stdin()
        .read_line(&mut input)
        .expect("Failed to read line");

    let number: i32 = match input.trim().parse() {
        Ok(num) => num,
        Err(_) => {
            println!("Invalid input, defaulting to 0");
            0
        }
    };

    println!("You entered: {}", number);
}
```

---

## Conclusion
On Day 1, you have learned:
- How to use associated functions like `String::new`, `Vec::new`, and `HashMap::new`.
- The difference between type-level and instance-level functions.
- Using enums like `Option` and `Result` for safe and explicit handling of optional values and errors.
- Reading integers from standard input using `io::stdin()`.

Keep experimenting with these concepts to deepen your understanding of Rust!


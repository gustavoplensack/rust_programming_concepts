# Chapter 3 notes

## Variables and Mutability

* Variables are declared with `let`;

* Variables are immutable by default, unless declared with `mut` keyword;

* Constants are declared with the `const` keyword and should be used evaluated in compile time;

* Shadowing is when you declare a variable is declared with the same name as previous using `let`. With shadowing we can use previuous value and use it inside a new scope created with a `{}`;

## Data Types

* Rust is a *statically typed language*, so we must know all the types in the compile time;

* Compile tries to infer the type if it is not provided, but sometimes you have to do it explicitely;

* Rust supports tuples, that are declared with `(x,y,z)`. The types of the tuple elements can vary;

* An empty tuple `()` is named an unit and is a special value returned by any function that do not have an explicit return value;

* A tuple element is acessed with `x.INDEX`, example:

```rust
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
```

* An array is a fixed size value collection, where all the values must have the same type. To declare an array you have to pass the size and data type. And its values are acessed just like in C. Example:

```rust
fn main() {
    let a: [i32; 5] = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```

* Rust is memory safe, so if you try to access an incorrect index (for example the 4th element of a 3-sized array) it raises an error idicating an out-of-bound array.

## Functions

* The `main` function is always the entrypoint for every rust program;

* Use the __snake_case__ naming convention for Rust functions and variables;

* Function syntax and usage really looks like C code;

* The function parameters type must be declared within the function;

* The type return value of a function is specified with an arrow `->`;

* The return value is the last expression in the function! Altough you can exit early using return;

### Statements

* Are instructions that perform some action and do not return a value;

* An example of statment:

```rust
    let x:u32 = 6;
```

### Expressions

Are instructions that evaluate to a resultant value.

* An example of expression:

```rust
    5 + 6;
```

* Calling a function, a macro or a scope block is an expression! For example the below code `y` is 4;

```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {y}");
}
```

* __NOTE:__ the line `x+1` do not have a semicolon at the end because it is a statement! If it had, it would be understood as an expression;

## Control flow

This is a common feature of all languages, is the ability to run some code given a condition.

### `if` expression

* The syntax is just like C;

* Unlike other languages, a condition must be a __boolean__, other types of values won't be automatically converted;

* It is possible to make it in an one-liner. But both values must be of the same type! Check an example below:

```rust
    let a = if condition { 5 } else { 6 }; // This is OK.
    let a = if condition { 5 } else { '6' }; // This is BAD. The compiler will indicate this as an error.
```

* __NOTE:__ we can't set different types for the same varialbe in an `if` expression and use it outside the if branches, as the compiler must know the type of the variable after the execution.

### Repetion loops

#### `loop` repetion

* This is a never ending loop, you must explictly break this using a `break`;

* In this case, using `continue` is also a good idea to skip some unwanted code an go to the next iteration;

* `loop`s can return values! One of the use cases of this operator is to retry an operation until it completed it's job and you may need the result of this operation. The return value must be provided after the `break`. Check how to do it:

```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

* When nesting loops, the `break` and `continue` operations are used in the innermost loop. In this case you can specify the outermost or any intermediary using the loop labeling. Check it out:

```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

### `while` repetition

* A `while` loop runs while the condition is `true`. It is useful because it cuts a lot of the need for conditional inside the loop to determine when to break it;

* The syntax looks like C:

```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

### `for` repetion

* Is the safest way to iterate over a collection, such as an array.

* The syntax looks like something between Python and C. Check it out:

```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

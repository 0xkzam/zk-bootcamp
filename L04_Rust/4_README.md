## Rust crash course

### Variables
The type of a variable is often inferred by the compiler, so it's not always mandatory to explicitly specify the type when declaring variables. However, the variable must be initialized at the time of declaration for the compiler to infer its type.

|   |   |
|---|---|
| Assignment | `let` |
| Mutability | By default, immutable. Can be made mutable by using mut keyword <br>`let mut x = 1;` <br> `x += 2; `|
| Shadowing | Allows a variable to be re-declared in the same scope with the same name <br> `let y = 4;` <br> `// Shadowing` <br> `let y = "I can also be bound to text!";`|
| De-structuring <br>assignments | `let tup = (3, 4);` <br>`let (x, _) = tup;` <br><br> `let array = [1, 2, 3, 4];` <br> `let [a, b, ..] = array;` | 
|Attributes | e.g. suppress unused variable warning <br>`#[allow(unused_variables)]` <br>`fn main() { let x = 1};`  |
|   |   |

### Data Types

#### 1. Scalar types (Represents single value)
|  |   |
|---|---|
| Integers |  i8 to i128, u8 to u128, isize, usize |
|Floating point numbers (signed)|f32, f64|
|Boolean|bool|
|Character (not a numeric type)|char|
|||
#### 2. Compound types (Primitive)
|  |   |
|---|---|
|Tuples|`let x: (i32, &str) = (1, "hello");`|
|Arrays (a fixed-size list of the same type)|`let a: [i32; 5] = [1, 2, 3, 4, 5];`|
|||
#### 3. Compound types (Custom)
|  |   |
|---|---|
|Struct|`struct Point { x: i32, y: i32, }`|
|Enum| `enum Character { Digit(i32), Other, }` <br> `let m = Character::Other` <br> Stadard enums: Option, Result |
|Vectors|`let v = vec![1, 2, 3];` <br> `let mut n: Vec<i32> = Vec::new();`|
|||
#### 4. Strings
  - Statically allocated, immutable string slices: `&str`
    - `let s = "Hello";`
  - Heap allocated, growable string object: `String`
    - `let mut s = "Hello".to_string();`
  - Use to_string() or String::from() to convert &str to String objects


### Functions

```rust
fn test(a: u32) -> bool {
    if a == 0 {
        return false;
    }
    a == 7
}
```

### If expressions
Note: not a statement as it can return a value.

```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };
    println!("The value of number is: {}", number);
}
```

### Loops
```rust
//inclusive end, inclusive end, every 2nd value
for n in (1..=101).step_by(2){ } 

//infinite loop
loop { }

//while loop
while num != 0 {
    num -= 1;
}
```
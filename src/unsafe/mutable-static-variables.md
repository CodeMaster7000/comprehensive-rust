# Mutable Static Variables

It is safe to read an immutable static variable:

```rust,editable
static HELLO_WORLD: &str = "Hello, world!";

fn main() {
    println!("HELLO_WORLD: {}", HELLO_WORLD);
}
```

However, since data races can occur, it is unsafe to read and write mutable
static variables:

```rust,editable
static mut COUNTER: u32 = 0;

fn add_to_counter(inc: u32) {
    unsafe { COUNTER += inc; }  // Potential data race!
}

fn main() {
    add_to_counter(42);

    unsafe { println!("COUNTER: {}", COUNTER); }  // Potential data race!
}
```

<details>

Using a mutable static is generally a bad idea, but there are some cases where it might make sense
in low-level `no_std` code, such as implementing a heap allocator or working with some C APIs.

</details>

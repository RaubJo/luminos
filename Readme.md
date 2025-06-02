# luminos

This is a Laravel inspired application framework.

This crate re-exports the following sub crates to provide a unified api.

- [luminos-Contracts](https://github.com/RaubJo/luminos-contracts)
- [luminos-Support](https://github.com/RaubJo/luminos-support)
- [luminos-Container](https://github.com/RaubJo/luminos-container)

The goal of this is provide a simple way to build runtime agnostic rust apps.

- Tauri
- Web (Rocket, Axum, Actix, etc.)

For the container singleton 
```rust
use std::collections::HashMap;
use std::sync::OnceLock;

fn hashmap() -> &'static HashMap<u32, &'static str> {
    static HASHMAP: OnceLock<HashMap<u32, &str>> = OnceLock::new();
    HASHMAP.get_or_init(|| {
        let mut m = HashMap::new();
        m.insert(0, "foo");
        m.insert(1, "bar");
        m.insert(2, "baz");
        m
    })
}

fn main() {
    // First access to `HASHMAP` initializes it
    println!("The entry for `0` is \"{}\".", hashmap().get(&0).unwrap());

    // Any further access to `HASHMAP` just returns the computed value
    println!("The entry for `1` is \"{}\".", hashmap().get(&1).unwrap());
}
```

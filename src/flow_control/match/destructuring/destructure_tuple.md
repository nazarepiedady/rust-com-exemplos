# Tuplas

As tuplas podem ser desestruturas num `match` da seguinte maneira:

```rust,editable
fn main() {
    let triple = (0, -2, 3);
    // TODO ^ Experimente valores diferentes para `triple`

    println!("Tell me about {:?}", triple);
    // A correspondência pode ser usada para desestruturar uma tupla
    match triple {
        // Desestruturar o segundo e o terceiro elemento
        (0, y, z) => println!("First is `0`, `y` is {:?}, and `z` is {:?}", y, z),
        (1, ..)  => println!("First is `1` and the rest doesn't matter"),
        (.., 2)  => println!("last is `2` and the rest doesn't matter"),
        (3, .., 4)  => println!("First is `3`, last is `4`, and the rest doesn't matter"),
        // `..` pode ser usado para ignorar o resto da tupla
        _      => println!("It doesn't matter what they are"),
        // `_` significa não vincular o valor à uma variável
    }
}
```

### Consulte também:

[Tuplas](../../../primitives/tuples.md)

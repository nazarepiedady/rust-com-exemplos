# Parecida com C

`enum` também pode ser usado como enumerações parecidas com C.

```rust,editable
// Um atributo para esconder os avisos de código não usado.
#![allow(dead_code)]

// enumeração com discriminador implícito (começa em 0)
enum Number {
    Zero,
    One,
    Two,
}

// enumeração com discriminador explícito
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}

fn main() {
    // `enums` podem ser moldados como inteiros.
    println!("zero is {}", Number::Zero as i32);
    println!("one is {}", Number::One as i32);

    println!("roses are #{:06x}", Color::Red as i32);
    println!("violets are #{:06x}", Color::Blue as i32);
}
```

### Consulte também:

[moldagem][cast]

[cast]: ../../types/cast.md

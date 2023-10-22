# Guardas

Uma *guarda* de `match` pode ser adicionada para filtrar o braço.

```rust,editable
#[allow(dead_code)]
enum Temperature {
    Celsius(i32),
    Fahrenheit(i32),
}

fn main() {
    let temperature = Temperature::Celsius(35);
    // ^ TODO experimento diferentes valores para `temperature`

    match temperature {
        Temperature::Celsius(t) if t > 30 => println!("{}C is above 30 Celsius", t),
        // A parte da condição if ^ é uma guarda
        Temperature::Celsius(t) => println!("{}C is below 30 Celsius", t),

        Temperature::Fahrenheit(t) if t > 86 => println!("{}F is above 86 Fahrenheit", t),
        Temperature::Fahrenheit(t) => println!("{}F is below 86 Fahrenheit", t),
    }
}
```

Nota que o compilador não levará as condições da guarda em consideração quando verificamos se todos os padrões estão cobertos pela expressão de correspondência.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let number: u8 = 4;

    match number {
        i if i == 0 => println!("Zero"),
        i if i > 0 => println!("Greater than zero"),
        // _ => unreachable!("Should never happen."),
        // TODO ^ remova o comentário para corrigir a compilação
    }
}
```

### Consulte Também:

[Tuplas](../../primitives/tuples.md)
[Enumerações](../../custom_types/enum.md)

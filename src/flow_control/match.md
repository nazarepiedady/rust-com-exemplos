# `match`

A Rust fornece correspondência de padrão através da palavra-chave `match`, que pode ser usada como uma `switch` de C. O primeiro braço de correspondência é avaliado e todos os valores possíveis devem ser cobertos.

```rust,editable
fn main() {
    let number = 13;
    // TODO ^ Tente valores diferentes para `number`

    println!("Tell me about {}", number);
    match number {
        // Corresponder um único valor
        1 => println!("One!"),
        // Corresponder vários valores
        2 | 3 | 5 | 7 | 11 => println!("This is a prime"),
        // TODO ^ Tente adicionar 13 à lista de valores primos
        // Corresponder um limite inclusivo
        13..=19 => println!("A teen"),
        // Lidar com o resto dos casos
        _ => println!("Ain't special"),
        // TODO ^ Tente comentar este braço de captura total
    }

    let boolean = true;
    // `match` também é uma expressão
    let binary = match boolean {
        // Os braços duma correspondência deve cobrir todos os valores possíveis
        false => 0,
        true => 1,
        // TODO ^ Tente comentar um destes braços
    };

    println!("{} -> {}", boolean, binary);
}
```

# laço de repetição

A Rust fornece uma palavra-chave `loop` para indicar um laço infinito.

A declaração `break` pode ser usada para sair dum laço de repetição a qualquer momento, ao passo que a declaração `continue` pode ser usada para ignorar o resto da iteração e começar uma nova.

```rust,editable
fn main() {
    let mut count = 0u32;

    println!("Let's count until infinity!");

    // Laço de repetição infinita
    loop {
        count += 1;

        if count == 3 {
            println!("three");

            // Ignorar o resto desta iteração
            continue;
        }

        println!("{}", count);

        if count == 5 {
            println!("OK, that's enough");

            // Sair deste laço de repetição
            break;
        }
    }
}
```
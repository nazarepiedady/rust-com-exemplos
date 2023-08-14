# `while let`

Semelhante ao `if let`, `while let` pode tornar sequências de `match` embaraçosas mais toleráveis. Considere a seguinte sequência que incrementa `i`:

```rust
// Tornar `optional` do tipo `Option<i32>`
let mut optional = Some(0);

// Tentar repetidamente este teste.
loop {
    match optional {
        // Se `optional` desestruturar, avalia o bloco.
        Some(i) => {
            if i > 9 {
                println!("Greater than 9, quit!");
                optional = None;
            } else {
                println!("`i` is `{:?}`. Try again.", i);
                optional = Some(i + 1);
            }
            // ^ Exige 3 indentações!
        },
        // Sair do laço de repetição quando a desestruturação falhar:
        _ => { break; }
        // ^ Porquê que isto deveria ser obrigatório? Deve existir um jeito melhor!
    }
}
```

O uso de `while let` torna esta sequência muito mais agradável:

```rust,editable
fn main() {
    // Tornar `optional` do tipo `Option<i32>`
    let mut optional = Some(0);

    // Isto lê-se: "enquanto `let` desestruturar `optional`" à
    // `Some(i)`, avaliar o bloco (`{}`). Se não `break`.
    while let Some(i) = optional {
        if i > 9 {
            println!("Greater than 9, quit!");
            optional = None;
        } else {
            println!("`i` is `{:?}`. Try again.", i);
            optional = Some(i + 1);
        }
        // ^ Menos desvio à direita e não exige
        // manipular explicitamente o caso de falha.
    }
    // ^ `if let` tinha cláusulas `else` ou `else if` opcionais adicionais
    // `while let` não tem estas.
}
```

### Consulte também:

[`enum`][enum], [`Option`][option], e o [RFC][while_let_rfc]

[enum]: ../custom_types/enum.md
[option]: ../std/option.md
[while_let_rfc]: https://github.com/rust-lang/rfcs/pull/214

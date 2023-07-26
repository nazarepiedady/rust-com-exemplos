# Âmbito e Obscurecimento

Os vínculos de variável têm um âmbito, e são obrigados a viver num *bloco*. Um bloco é uma coleção de declarações fechadas por chavetas `{}`.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Este vínculo vive na função principal
    let long_lived_binding = 1;

    // Isto é um bloco, e tem um âmbito mais pequeno do que a função principal
    {
        // Este vínculo apenas existe neste bloco
        let short_lived_binding = 2;

        println!("inner short: {}", short_lived_binding);
    }
    // Fim do bloco

    // Erro! `short_lived_binding` não existe neste âmbito
    println!("outer short: {}", short_lived_binding);
    // FIXME ^ Comente esta linha

    println!("outer long: {}", long_lived_binding);
}
```

Além disto, [obscurecimento de variável][variable-shadow] é permitido.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let shadowed_binding = 1;

    {
        println!("before being shadowed: {}", shadowed_binding);

        // Este vínculo *obscurece* aquela que está no exterior
        let shadowed_binding = "abc";

        println!("shadowed in inner block: {}", shadowed_binding);
    }
    println!("outside inner block: {}", shadowed_binding);

    // Este vínculo *obscurece* o vínculo anterior
    let shadowed_binding = 2;
    println!("shadowed in outer block: {}", shadowed_binding);
}
```

[variable-shadow]: https://en.wikipedia.org/wiki/Variable_shadowing

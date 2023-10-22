# Vínculo

Acessar indiretamente uma variável torna impossível ramificar e usar esta variável sem re-vincular. `match` fornece o símbolo `@` para vincular os valores aos nomes:

```rust,editable
// Uma função `age` que retorna uma `u32`.
fn age() -> u32 {
    15
}

fn main() {
    println!("Tell me what type of person you are");

    match age() {
        0             => println!("I haven't celebrated my first birthday yet"),
        // Poderia `match` 1 ..= 12 diretamente mas então de qual
        // idade seria a criança? Ao invés disto, vinculamos ao `n`
        // para a sequência de 1 ..= 12. Agora a idade pode ser reportada.
        n @ 1  ..= 12 => println!("I'm a child of age {:?}", n),
        n @ 13 ..= 19 => println!("I'm a teen of age {:?}", n),
        // Nada vinculado. Retorna o resultado.
        n             => println!("I'm an old person of age {:?}", n),
    }
}
```

You can also use binding to "destructure" `enum` variants, such as `Option`:
Nós também podemos usar o vínculo para "desestruturar" as variantes de `enum`, tais como `Option`:

```rust,editable
fn some_number() -> Option<u32> {
    Some(42)
}

fn main() {
    match some_number() {
        // Recebeu a variante `Some`, corresponde se seu valor,
        // vinculado à `n`, é igual à 42.
        Some(n @ 42) => println!("The Answer: {}!", n),
        // Corresponde qualquer outro número.
        Some(n)      => println!("Not interesting... {}", n),
        // Corresponde mais alguma coisa (variante `None`).
        _            => (),
    }
}
```

### Consulte Também:

[`functions`][functions], [`enums`][enums] e [`Option`][option]

[functions]: ../../fn.md
[enums]: ../../custom_types/enum.md
[option]: ../../std/option.md

# Ponteiros ou Referência

Para os ponteiros, uma distinção precisa de ser feita entre a desestruturação e a destruição de referência, uma vez que são conceitos diferentes que são usados de maneira diferente nas linguagens como C/C++.

* A destruição de referência usa `*`
* A desestruturação usa `&`, `ref`, e `ref mut`

```rust,editable
fn main() {
    // Atribuir uma referência do tipo `i32`. O `&` significa que
    // existe uma referência a ser atribuída.
    let reference = &4;

    match reference {
        // Se `reference` for o padrão correspondente contra `&val`,
        // resulta numa comparação como:
        // `&i32`
        // `&val`
        // ^ Nós vemos que se os `&` correspondentes forem eliminados,
        // então deve ser atribuído à `val`.
        &val => println!("Got a value via destructuring: {:?}", val),
    }

    // Para evitar o `&`, destruímos a referência antes da correspondência.
    match *reference {
        val => println!("Got a value via dereferencing: {:?}", val),
    }

    // E se não começarmos com uma referência? `reference` era um `&`
    // porque o lado direito já era uma referência. Isto não é uma
    // referência porque o lado direito não é uma.
    let _not_a_reference = 3;

    // A Rust fornece `ref` para exatamente este propósito. Ela modifica a
    // atribuição para que uma referência seja criada para o elemento;
    // esta referência é atribuída.
    let ref _is_a_reference = 3;

    // Assim, ao definir 2 valores sem referência, as referências podem
    // ser recuperadas através de `ref` e `ref mut`.
    let value = 5;
    let mut mut_value = 6;

    // Usar a palavra-chave `ref` para criar uma referência
    match value {
        ref r => println!("Got a reference to a value: {:?}", r),
    }

    // Usar `ref mut` de maneira semelhante.
    match mut_value {
        ref mut m => {
            // Temos uma referência. Temos que destruir a sua referência
            // antes que possamos adicionar qualquer coisa à ela.
            *m += 10;
            println!("We added 10. `mut_value`: {:?}", m);
        },
    }
}
```

### Consulte também:

[O padrão de referência](../../../scope/borrow/ref.md)

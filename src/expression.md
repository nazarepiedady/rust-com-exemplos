# Expressões

Um programa de Rust é (maioritariamente) composto duma série de declarações e expressões:

```rust,editable
fn main() {
    // declaração
    // declaração
    // declaração
}
```

Existem alguns tipos de declarações na Rust. Os dois mais comuns são declaração dum vínculo de variável, e o uso dum `;` com expressão:

```rust,editable
fn main() {
    // vínculo de variável
    let x = 5;

    // expressão;
    x;
    x + 1;
    15;
}
```

Os blocos são também expressões, então podem ser usados como valores em atribuições. A última expressão no bloco serão atribuídos à expressão do local tal como uma variável local. No entanto, se a última expressão do bloco termina com um sinal de ponto e vírgula, o valor de retorno será `()`:

```rust,editable
fn main() {
    let x = 5u32;

    let y = {
        let x_squared = x * x;
        let x_cube = x_squared * x;

        // Esta expressão será atribuída à `y`
        x_cube + x_squared + x
    };

    let z = {
        // O ponto e vírgula suprime esta expressão e `()` é atribuído à `z`
        2 * x;
    };

    println!("x is {:?}", x);
    println!("y is {:?}", y);
    println!("z is {:?}", z);
}
```

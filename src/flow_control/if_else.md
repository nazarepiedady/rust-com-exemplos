# `if` ou `else`

A ramificação com `if` ou `else` é semelhante às outras linguagens. Ao contrário delas, a condição booleana não precisa ser envolvida por parênteses, e cada condição é seguida por um bloco. As condicionais `if` e `else` são expressões, e todos os ramos deve retornar o mesmo tipo.

```rust,editable
fn main() {
    let n = 5;

    if n < 0 {
        print!("{} is negative", n);
    } else if n > 0 {
        print!("{} is positive", n);
    } else {
        print!("{} is zero", n);
    }

    let big_n =
        if n < 10 && n > -10 {
            println!(", and is a small number, increase ten-fold");

            // Esta expressão retorna uma `i32`.
            10 * n
        } else {
            println!(", and is a big number, halve the number");

            // Esta expressão deve retornar também uma `i32`.
            n / 2
            // TODO ^ Tente suprimir esta expressão com um ponto e vírgula.
        };
    //   ^ Não esqueça do ponto e vírgula! Todos vínculos de `let` precisam.

    println!("{} -> {}", n, big_n);
}
```

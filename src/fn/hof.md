# Funções de Ordem Superior

A Rust fornece Funções de Ordem Superior (HOF, sigla em Inglês). Estas são funções que recebem um ou mais funções e ou produzem uma função mais útil. As funções de ordem superior e iteradores preguiçosos dão à Rust o seu sabor funcional:

```rust,editable
fn is_odd(n: u32) -> bool {
    n % 2 == 1
}

fn main() {
    println!("Find the sum of all the squared odd numbers under 1000");
    let upper = 1000;

    // Abordagem imperativa
    // Declarar variável acumuladora
    let mut acc = 0;
    // Iterar: 0, 1, 2, ... à infinito
    for n in 0.. {
        // Fazer a quadratura do número
        let n_squared = n * n;

        if n_squared >= upper {
            // Quebrar o laço se excedido o limite superior
            break;
        } else if is_odd(n_squared) {
            // Acumular o valor, se for ímpar
            acc += n_squared;
        }
    }
    println!("imperative style: {}", acc);

    // Abordagem funcional
    let sum_of_squared_odd_numbers: u32 =
        (0..).map(|n| n * n)                             // Todos os números naturais ao quadrado
             .take_while(|&n_squared| n_squared < upper) // Abaixo do limite superior
             .filter(|&n_squared| is_odd(n_squared))     // Que são ímpares
             .sum();                                     // Some-os
    println!("functional style: {}", sum_of_squared_odd_numbers);
}
```

[Option][option] e [Iterator][iter] implementam a sua parte clara de funções de ordem superior.

[option]: https://doc.rust-lang.org/core/option/enum.Option.html
[iter]: https://doc.rust-lang.org/core/iter/trait.Iterator.html

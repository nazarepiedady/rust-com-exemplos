# Funções Divergentes

As funções divergentes nunca retornam. Elas são marcadas usando `!`, o qual é um tipo vazio.

```rust
fn foo() -> ! {
    panic!("This call never returns.");
}
```

Em oposição à todos os outros tipos, esta não pode ser instanciada, porque o conjunto de todos os possíveis valores que este tipo pode ter é vazio. Nota que, é diferente do tipo `()`, que tem exatamente um valor possível.

Por exemplo, esta função retorna de costume, embora não exista informação no valor de retorno:

```rust
fn some_fn() {
    ()
}

fn main() {
    let _a: () = some_fn();
    println!("This function returns and you can see this line.");
}
```

Em posição à esta função, que nunca retornará o controlo de volta ao chamador.

```rust,ignore
#![feature(never_type)]

fn main() {
    let x: ! = panic!("This call never returns.");
    println!("You will never see this line!");
}
```

Embora isto possa parecer como um conceito abstrato, é de fato muito útil e muitas vezes prático. A principal vantagem deste tipo é que pode ser fundido à qualquer outro e, portanto usado em lugares onde um tipo exato é obrigatório, por exemplo nos ramos de `match`. Isto permite-nos escrever código como este:

```rust
fn main() {
    fn sum_odd_numbers(up_to: u32) -> u32 {
        let mut acc = 0;
        for i in 0..up_to {
            // Repara que o tipo de retorno desta expressão de correspondência
            // de ser u32 por causa do tipo da variável "addition".
            let addition: u32 = match i%2 == 1 {
                // A variável "i" é do tipo u32, que está perfeitamente correta.
                true => i,
                // Por outro lado, a expressão "continue" não retorna u32,
                // mas ainda está bem, porque nunca retorna e portanto não viola os
                // requisitos da expressão de correspondência.
                false => continue,
            };
            acc += addition;
        }
        acc
    }
    println!("Sum of odd numbers up to 9 (excluding): {}", sum_odd_numbers(9));
}
```

Ela também é o tipo de retorno das função que percorrem os laços de repetição para sempre (por exemplo, `loop {}`) tal como servidores de rede ou funções que terminam o processo (por exemplo, `exit()`).

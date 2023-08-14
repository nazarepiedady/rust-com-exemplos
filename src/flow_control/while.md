# `while`

A palavra-chave `while` pode ser usada para executar um laço de repetição enquanto (`while`) uma condição for verdadeira.

Vamos escrever o infame [FizzBuzz][fizzbuzz] usando um laço de repetição `while`.

```rust,editable
fn main() {
    // Uma variável contadora
    let mut n = 1;

    // Laço de repetição enquanto `n` for menor do que 101 
    while n < 101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }

        // Incrementar contador
        n += 1;
    }
}
```

[fizzbuzz]: https://en.wikipedia.org/wiki/Fizz_buzz

# Funções

Funções são declaradas usando a palavra-chave `fn`. Seus argumentos são anotados com tipagem assim como variáveis, e se a função retorna algum valor, o tipo de retorno deve ser especificado após uma flecha `->`.

A expressão final de uma função será usada como valor de retorno. Alternativamente, você pode usar `return` para retornar um valor no meio da função, até mesmo dentro de loops ou `if`s.

Vamos reescrever o FizzBuzz usando funções:

```rust,editable
// Diferente de C e C++, não existe restrição na ordem das definições das funções
fn main() {
    // Podemos usar a função aqui, e definir ela depois em outro local
    fizzbuzz_to(100);
}

// Uma função que retorna um valor boleano
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    // Caso específico, retorne antes
    if rhs == 0 {
        return false;
    }

    // Isso é a última expressão, então a palavra-chave `return` não é necessária
    lhs % rhs == 0
}

// Funções que "não" retornam um valor, na verdade, retornam o tipo unitário `()`
fn fizzbuzz(n: u32) -> () {
    if is_divisible_by(n, 15) {
        println!("fizzbuzz");
    } else if is_divisible_by(n, 3) {
        println!("fizz");
    } else if is_divisible_by(n, 5) {
        println!("buzz");
    } else {
        println!("{}", n);
    }
}

// Quando uma função retorna `()`, o tipo pode ser omitido da assinatura
fn fizzbuzz_to(n: u32) {
    for n in 1..=n {
        fizzbuzz(n);
    }
}
```

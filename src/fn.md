# Funções

As funções são declaras usando a palavra-chave `fn`. Os seus argumentos têm os tipos anotados, tal como as variáveis, e se a função retornar um valor, o tipo de retorno de ser especificado depois duma flecha (ou seta) `->`.

A expressão final numa função será usada como valor de retorno. Alternativamente, a declaração de `return` pode ser usada para retornar um valor mais cedo a partir de dentro da função, até mesmo a partir de dentro dos laços de repetição ou declarações de `if`.

Vamos reescrever o FizzBuzz usando funções!:

```rust,editable
// Diferente de C e C++,
// não existe restrição sobre a ordem de definições de função
fn main() {
    // Nós podemos usar esta função,
    // e defini-la em algum lugar depois
    fizzbuzz_to(100);
}

// Função que retorna um valor booleano
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    // Caso extremo, retornar prematuramente
    if rhs == 0 {
        return false;
    }

    // Isto é uma expressão,
    // a palavra-chave `return` não é necessária
    lhs % rhs == 0
}

// As funções que "não" retornam um valor,
// na realidade retornam o tipo unitário `()`
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

// Quando uma função retornar `()`,
// o tipo de retorno pode ser omitido da assinatura
fn fizzbuzz_to(n: u32) {
    for n in 1..=n {
        fizzbuzz(n);
    }
}
```

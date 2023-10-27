# Literais e Operadores

Os inteiros `1`, flutuantes `1.2`, caracteres `'a'`, sequências de caracteres `"abc"`, booleanos `true` e o tipo unitário `()` podem ser expressados usando literais.

Os inteiros podem, alternativamente, ser expressados usando a notação hexadecimal, octal ou binária usando estes prefixos respetivamente: `0x`, `0o` ou `0b`.

Os sublinhados podem ser inseridos nos literais numéricos para melhorar a legibilidade, por exemplo `1_000` é o mesmo que `1000`, e `0.000_001` é o mesmo que `0.000001`.

A Rust suporta a [notação cientifica e][enote], por exemplo `1e6`, `7.6e-4`. O tipo associado é `f64`.

Nós precisamos dizer ao compilador o tipo dos literais que usamos. Por agora, usaremos o sufixo `u32` para indicar que o literal é um inteiro de 32-bit sem sinal, e o sufixo `i32` para indicar que é um inteiro de 32-bit com sinal.

Os operadores disponíveis e suas precedências [na Rust][rust op-prec] são semelhantes às outras [linguagens parecidas com C][op-prec]:

```rust,editable
fn main() {
    // Adição de inteiro
    println!("1 + 2 = {}", 1u32 + 2);

    // Subtração de inteiro
    println!("1 - 2 = {}", 1i32 - 2);
    // TODO ^ Tente mudar `1i32` para `1u32` para veres a importância do tipo

    // Notação cientifica
    println!("1e4 is {}, -2.5e-3 is {}", 1e4, -2.5e-3);

    // Lógica booleana de curto-circuito
    println!("true AND false is {}", true && false);
    println!("true OR false is {}", true || false);
    println!("NOT true is {}", !true);

    // Operações bitwise
    println!("0011 AND 0101 is {:04b}", 0b0011u32 & 0b0101);
    println!("0011 OR 0101 is {:04b}", 0b0011u32 | 0b0101);
    println!("0011 XOR 0101 is {:04b}", 0b0011u32 ^ 0b0101);
    println!("1 << 5 is {}", 1u32 << 5);
    println!("0x80 >> 2 is 0x{:x}", 0x80u32 >> 2);

    // Use sublinhados para melhorar a legibilidade!
    println!("One million is written as {}", 1_000_000u32);
}
```

[enote]: https://en.wikipedia.org/wiki/Scientific_notation#E_notation
[rust op-prec]: https://doc.rust-lang.org/reference/expressions.html#expression-precedence
[op-prec]: https://en.wikipedia.org/wiki/Operator_precedence#Programming_languages

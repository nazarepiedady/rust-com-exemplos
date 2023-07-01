# Impressão Formatada

A impressão é manipulada por uma série de [`macros`][macros] definidas na [`std::fmt`][fmt], algumas das quais incluem:

* `format!`: escreve o texto formatado para a [`String`][string].
* `print!`: o mesmo que `format!` mas o texto é imprimido para a consola (`io::stdout`).
* `println!`: o mesmo que `print!` mas uma nova linha é anexada.
* `eprint!`: o mesmo que `print!` mas o texto é imprimido para o erro padrão (`io::stderr`).
* `eprintln!`: o mesmo que `eprint!` mas uma nova linha é anexada.

Todos analisam o texto da mesma maneira. Como uma vantagem, a Rust verifica a exatidão da formatação em tempo de compilação:

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Em geral, as `{}` serão automaticamente substituídas por quaisquer
    // argumentos. Estes serão convertidos em sequências de caracteres.
    println!("{} days", 31);

    // Os argumentos posicionais podem ser usados. Especificar um inteiro
    // dentro de `{}` determina qual argumento adicional será substituído.
    // Os argumentos começam em 0 imediatamente depois da 
    // sequência de caracteres de formatação.
    println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");

    // As can named arguments.
    println!("{subject} {verb} {object}",
             object="the lazy dog",
             subject="the quick brown fox",
             verb="jumps over");

    // Uma formatação diferente pode ser invocada com a especificação do
    // carácter de formato depois dum `:`.
    println!("Base 10:               {}",   69420); // 69420
    println!("Base 2 (binary):       {:b}", 69420); // 10000111100101100
    println!("Base 8 (octal):        {:o}", 69420); // 207454
    println!("Base 16 (hexadecimal): {:x}", 69420); // 10f2c
    println!("Base 16 (hexadecimal): {:X}", 69420); // 10F2C

    // Podemos justificar o texto à direita com uma largura especificada.
    // Isto resultará em "    1".
    // (Quatro espaços em branco e um "1", para uma largura total de 5).
    println!("{number:>5}", number=1);

    // Podemos acolchoar números com zeros adicionais,
    println!("{number:0>5}", number=1); // 00001
    // e ajustar à esquerda com a virada do sinal. Isto resultará em "10000".
    println!("{number:0<5}", number=1); // 10000

    // Podemos usar argumentos nomeados no 
    // especificador de formato anexando um `$`.
    println!("{number:0>width$}", number=1, width=5);

    // A Rust ainda verifica para certificar-se 
    // que o número correto de argumentos são usados.
    println!("My name is {0}, {1} {0}", "Bond");
    // FIXME ^ Add the missing argument: "James"

    // Apenas tipos que implementam `fmt::Display` podem ser formatados com `{}`.
    // Os tipos definidos pelo utilizador 
    // não implementam `fmt::Display` por padrão.

    #[allow(dead_code)] // desativa `dead_code` que alerta sobre módulo não usado.
    struct Structure(i32);

    // Isto não compilará porque `Structure` não implementa `fmt::Display`
    // println!("This struct `{}` won't print...", Structure(3));
    // TODO ^ Try uncommenting this line

    // Para a Rust 1.58 e acima, podemos capturar diretamente o argumento duma
    // variável envolvente. Tal como acima, isto resultará em "    1",
    // 4 espaços em branco e um "1".
    let number: f64 = 1.0;
    let width: usize = 5;
    println!("{number:>width$}");
}
```

O [`std::fmt`][fmt] contém muitas [`traits`][traits] que governam a exibição do texto. A forma de base de dois importantes são listados abaixo:

* `fmt::Debug`: Usa o marcador `{:?}`. Formata o texto para fins de depuração.
* `fmt::Display`: Usa o marcador `{}`. Formata o texto duma maneira mais elegante e agradável para o utilizador.

Cá, usamos `fmt::Display` porque a biblioteca `std` fornece implementações para estes tipos. Para imprimir texto para tipos personalizados, mais passos são necessários.

Implementar a característica `fmt::Display` implementa automaticamente a característica [`ToString`] que permite-nos [converter][convert] o tipo para [`String`][string].

Na *linha 46*, `#[allow(dead_code)]` é um [atributo][attribute] que apenas aplica-se ao módulo depois deste.

### Atividades

* Corrija o problema no código acima (vê a FIXME) para que esta execute sem erro.
* Tente desfazer o comentário da linha que tenta formatar a estrutura `Structure` (vê TODO)
* Adicione uma chamada de macro `println!` que imprime: `Pi is roughly 3.142` controlando o número de casas decimais exibido. Para os fins deste exercício, use `let pi = 3.141592` como uma estimativa para o pi. (Dica: podemos precisar de consultar a documentação de [`std::fmt`][fmt] para definir o número de decimais à exibir).

### Consulte também:

[`std::fmt`][fmt], [`macros`][macros], [`struct`][structs], [`traits`][traits], e [`dead_code`][dead_code].

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md
[attribute]: ../attribute.md
[dead_code]: ../attribute/unused.md

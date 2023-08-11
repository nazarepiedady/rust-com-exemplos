# Para e a partir de Sequências de Caracteres

## Converter para Sequência de Caracteres

Converter qualquer tipo para uma `String` é tão simples quando implementar a característica [`ToString`] para o tipo. Ao invés de fazer isto diretamente, deves implementar a característica [`fmt::Display`][Display] que auto-magicamente fornece [`ToString`] e também permite imprimir o tipo conforme discutidos na seção [`print!`][print].

```rust,editable
use std::fmt;

struct Circle {
    radius: i32
}

impl fmt::Display for Circle {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "Circle of radius {}", self.radius)
    }
}

fn main() {
    let circle = Circle { radius: 6 };
    println!("{}", circle.to_string());
}
```

## Analisando uma Sequência de Caracteres

Um dos tipos mais comum a converter para uma sequência de caracteres é um número. A abordagem idiomática para isto é usar a função [`parse`] e ou organizar para a inferência de tipo ou especificar o tipo a analisar usando a sintaxe 'turbofish'. Ambas alternativas são mostradas no seguinte exemplo. 

Isto converterá a sequência de caracteres para o tipo especificado enquanto a característica [`FromStr`] é implementada para este tipo. Isto é implementado para numerosos tipos dentro da biblioteca padrão. Para obter esta funcionalidade num tipo definido pelo utilizador simplesmente implemente a característica [`FromStr`] para este tipo.

```rust,editable
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed = "10".parse::<i32>().unwrap();

    let sum = parsed + turbo_parsed;
    println!("Sum: {:?}", sum);
}
```

[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[Display]: https://doc.rust-lang.org/std/fmt/trait.Display.html
[print]: ../hello/print.md
[`parse`]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`FromStr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html

# Formatação

Nós vimos que a formatação é especificada através de uma *sequência de caracteres de formatação*:

* `format!("{}", foo)` -> `"3735928559"`
* `format!("0x{:X}", foo)` -> [`"0xDEADBEEF"`][deadbeef]
* `format!("0o{:o}", foo)` -> `"0o33653337357"`

A mesma variável (`foo`) pode ser formatada diferentemente dependendo do qual *tipo de argumento* é usado: `X` vs `o` vs *não especificado*.

Esta funcionalidade de formatação é implementada através das características, e existe uma característica para cada tipo de argumento. A característica de formatação mais comum é `Display`, que lida com os casos onde o tipo do argumento é deixado não especificado: `{}` por exemplo.

```rust,editable
use std::fmt::{self, Formatter, Display};

struct City {
    name: &'static str,
    // Latitude
    lat: f32,
    // Longitude
    lon: f32,
}

impl Display for City {
    // `f` é um amortecedor, e este método deve escrever a
    // sequência de caracteres de formatação para ela.
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // `write!` é como `format!`, mas escreverá a sequência de caracteres de
        // formatação para um amortecedor (o primeiro argumento).
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.name, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

#[derive(Debug)]
struct Color {
    red: u8,
    green: u8,
    blue: u8,
}

fn main() {
    for city in [
        City { name: "Dublin", lat: 53.347778, lon: -6.259722 },
        City { name: "Oslo", lat: 59.95, lon: 10.75 },
        City { name: "Vancouver", lat: 49.25, lon: -123.1 },
    ] {
        println!("{}", city);
    }
    for color in [
        Color { red: 128, green: 255, blue: 90 },
        Color { red: 0, green: 3, blue: 254 },
        Color { red: 0, green: 0, blue: 0 },
    ] {
        // Troque isto para usar {} uma vez que tiveres adicionado uma
        // implementação para `fmt::Display`.
        println!("{:?}", color);
    }
}
```

Tu podes ver uma [lista completa de características de formatação][fmt_traits] e seus tipos de argumentos na documentação da [`std::fmt`][fmt].

### Atividade

Adicione uma implementação da característica `fmt::Display` para a estrutura `Color` acima para que a saída exiba algo como:

```text
RGB (128, 255, 90) 0x80FF5A
RGB (0, 3, 254) 0x0003FE
RGB (0, 0, 0) 0x000000
```

Duas sugestões caso ficares sem saber o que fazer:

* Tu [podes precisar de listar cada cor mais de uma vez][named_parameters].
* Tu podes [acolchoar com zeros para uma largura de 2][fmt_width] com `:0>2`.

### Consulte também:

[`std::fmt`][fmt]

[named_parameters]: https://doc.rust-lang.org/std/fmt/#named-parameters
[deadbeef]: https://en.wikipedia.org/wiki/Deadbeef#Magic_debug_values
[fmt]: https://doc.rust-lang.org/std/fmt/
[fmt_traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[fmt_width]: https://doc.rust-lang.org/std/fmt/#width

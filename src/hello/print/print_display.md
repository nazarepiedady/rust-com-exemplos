# Exibição

`fmt::Debug` dificilmente parece compacto e limpo, então é frequentemente vantajoso personalizar a aparência da saída. Isto é feito implementando manualmente a [`fmt::Display`][fmt], que usa o marcador de impressão `{}`. Sua implementação parece-se com:

```rust
// Importar (através de `use`) o módulo `fmt`
// para torná-lo disponível.
use std::fmt;

// Definir uma estrutura para qual `fmt::Display` será implementado.
// Isto é uma estrutura de tupla nomeada `Structure` que contém um `i32`.
struct Structure(i32);

// Para usar o marcador `{}`, a característica `fmt::Display`
// deve ser implementada manualmente para o tipo.
impl fmt::Display for Structure {
    // Esta característica exige `fmt` com esta exata assinatura.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Escrever estritamente o primeiro elemento para a corrente
        // de saída fornecida: `f`. Retorna `fmt::Result` que indica se
        // a operação foi bem-sucedida ou falhou. Nota que `write!` usa
        // sintaxe que é muito semelhante ao `println!`.
        write!(f, "{}", self.0)
    }
}
```

`fmt::Display` pode ser mais claro do que `fmt::Debug` mas isto apresenta um problema para a biblioteca `std`. Como deveriam os tipos ambíguos ser exibidos? Por exemplo, se a biblioteca `std` implementasse um único estilo para todos os `Vec<T>`, qual estilo seria? Seria qualquer destes dois?

* `Vec<path>`: `/:/etc:/home/username:/bin` (separa-se nos `:`)
* `Vec<number>`: `1,2,3` (separa-se nas `,`)

Não, porque não existe estilo ideal para todos os tipos e a biblioteca `std` não presume import uma. `fmt::Display` não é implementada para `Vec<T>` ou para quaisquer outros contentores genéricos. `fmt::Debug` deve então ser usado para estes casos genéricos.

Isto não é um problema embora porque para qualquer tipo de *contentor* novo que *não* é genérico, `fmt::Display` pode ser implementado:

```rust,editable
use std::fmt; // Importar `fmt`

// Uma estrutura segurando dois números. `Debug` será derivado assim os
// resultados podem ser contrastados com `Display`.
#[derive(Debug)]
struct MinMax(i64, i64);

// Implementar `Display` para `MinMax`.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Usar `self.number` para fazer referência à cada ponto de
        // dados posicional.
        write!(f, "({}, {})", self.0, self.1)
    }
}

// Definir uma estrutura onde os campos são nomeáveis para comparação.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// De maneira semelhante, implementar `Display` para `Point2D`.
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Personalizar, assim apenas `x` e `y` são denotados.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Compare structures:");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("The big range is {big} and the small is {small}",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Compare points:");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // Erro. Ambos `Debug` e `Display` foram implementados, mas `{:b}`
    // exige que `fmt::Binary` seja implementado. Isto não funcionará.
    // println!("What does Point2D look like in binary: {:b}?", point);
}
```

Assim, `fmt::Display` tem sido implementado mas `fmt::Binary` não tem, e portanto não pode ser usado. `std::fmt` tem vários tal como [`traits`][traits] e cada um exige sua própria implementação. Isto é detalhado mais adiante em [`std::fmt`][fmt].

### Atividade

Depois de verificar a saída do exemplo acima, use a estrutura `Point2D` como um guia para adicionar uma estrutura `Complex` ao exemplo. Quando imprimida da mesma maneira, a saída deveria ser:

```txt
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
```

### Consulte também:

[`derive`][derive], [`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
[`trait`][traits], e [`use`][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[use]: ../../mod/use.md

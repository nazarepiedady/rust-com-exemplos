# Enumerações

A palavra-chave `enum` permite a criação dum tipo que pode ser um das poucas variantes diferentes. Qualquer que é válido como uma `struct` é também válido numa `enum`.

```rust,editable
// Criar uma `enum` para classificar um evento de Web.
// Nota como nomes e informação juntos especificar a variante:
// `PageLoad != PageUnload` e `KeyPress(char) != Paste(String)`.
// Cada um é diferente e independente.
enum WebEvent {
    // Uma variante `enum` pode ser qualquer`unit-like`,
    PageLoad,
    PageUnload,
    // como estruturas de tupla,
    KeyPress(char),
    Paste(String),
    // ou estruturas parecidas de C.
    Click { x: i64, y: i64 },
}

// Uma função que recebe uma enumeração `WebEvent` como
// um argumento e não retorna nada.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("page loaded"),
        WebEvent::PageUnload => println!("page unloaded"),
        // Desestruturar `c` a partir duma variante `enum`.
        WebEvent::KeyPress(c) => println!("pressed '{}'.", c),
        WebEvent::Paste(s) => println!("pasted \"{}\".", s),
        // Desestruturar `Click` para `x` e `y`.
        WebEvent::Click { x, y } => {
            println!("clicked at x={}, y={}.", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // `to_owned()` cria uma `String` própria a partir
    // dum pedaço de sequência de caracteres.
    let pasted  = WebEvent::Paste("my text".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}

```

## Pseudónimos de Tipo

Se usas um pseudónimo de tipo, podes fazer referência a cada variante de enumeração através do pseudónimo. Isto pode ser útil se o nome da enumeração for muito longo ou muito genérico, e queres renomeá-lo.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// Creates a type alias
// Cria um pseudónimo de tipo
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    // Nós podemos fazer referência a cada variante através do pseudónimo,
    // e não seu nome longo e inconveniente.
    let x = Operations::Add;
}
```

O lugar mais comum que verás isto é em blocos `impl` usando o pseudónimo `Self`.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

Para saberes mais sobre as enumerações e pseudónimos de tipo, podes ler o [relatório de estabilização][aliasreport] a partir de quando esta funcionalidade foi estabilizada para Rust.

### Consulte também:

[`match`][match], [`fn`][fn], e [`String`][str], [RFC dos "Pseudónimos de tipo e variantes de enumeração" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html

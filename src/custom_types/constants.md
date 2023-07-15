# Constantes

A Rust tem dois tipos diferentes de constantes que podem ser declarados em qualquer âmbito incluindo global. Ambos exigem anotação de tipo explícita:

* `const`: Um valor não modificável (o caso comum).
* `static`: Uma variável possivelmente mutável com a vida útil de [`'static`][static].
  - A vida útil estática é inferida e não precisa de ser especificada.
  - O acesso ou modificação duma variável estática mutável é [`unsafe`][unsafe].

```rust,editable,ignore,mdbook-runnable
// As globais são declaradas fora de todos os outros âmbitos.
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    // Acessar constante em alguma função
    n > THRESHOLD
}

fn main() {
    let n = 16;

    // Acessar constante na linha principal
    println!("This is {}", LANGUAGE);
    println!("The threshold is {}", THRESHOLD);
    println!("{} is {}", n, if is_big(n) { "big" } else { "small" });

    // Erro! Não possível modificar uma `const`.
    THRESHOLD = 5;
    // FIXME ^ Comente esta linha
}
```

### Consulte também:

[O RFC de `const`/`static`](https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md), [vida útil da `'static`][static].

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md

# Primitivos

A Rust fornece acesso à uma grande variedade de `primitives`. Um amostra inclui:

### Tipos Escalares

* Inteiros com sinais:
* Inteiros sem sinais:
* Ponto flutuante
* Os valores escalares de código universal de `char` como `'a'`, `'α'` e `'∞'` (são 4 bytes cada)
* `bool` ou é `true` ou é `false`
* O tipo de unitário `()`, cujo único valor possível é uma tupla vazia: `()`

Apesar do valor dum tipo unitário ser uma tupla, não é considerado um tipo composto porque não contém vários valores.

### Tipos Compostos

* Arranjos como `[1, 2, 3]`
* Tuplas como `(1, true)`

As variáveis podem sempre ser *anotadas por tipo*. Os números podem adicionalmente ser anotados através dum *sufixo* ou *por padrão*. Os inteiros predefine para `i32` e flutuantes para `f64`. Nota que a Rust também pode inferir tipos a partir do contexto:

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Variáveis podem ser anotadas por tipo.
    let logical: bool = true;

    let an_integer   = 5i32; // Suffix annotation Anotação de sufixo

    // Ou um padrão será usado.
    let default_float   = 3.0; // `f64`
    let default_integer = 7;   // `i32`

    // Um tipo também pode ser inferido a partir do contexto.
    let mut inferred_type = 12; // O tipo i64 é inferido a partir da outra linha.
    inferred_type = 4294967296i64;

    // Um valor da variável mutável pode ser mudado.
    let mut mutable = 12; // `i32` mutável
    mutable = 21;

    // Erro! O tipo duma variável não pode ser mudado.
    mutable = true;

    // As variáveis podem ser sobrescritas com obscurecimento.
    let mutable = true;
}
```

### Consulte também:

[a biblioteca `std`][std], [`mut`][mut], [`inference`][inference], e
[`shadowing`][shadowing]

[std]: https://doc.rust-lang.org/std/
[mut]: variable_bindings/mut.md
[inference]: types/inference.md
[shadowing]: variable_bindings/scope.md

# Depuração

Todos os tipos que quiserem usar `traits` de formatação de `std::fmt` exigem que uma implementação seja imprimível. Implementações automáticas são apenas fornecidas para tipos tais como na biblioteca `std`. Todos os outros *devem* ser manualmente implementados de alguma maneira.

A `trait` de `fmt::Debug` torna isto muito direto. *Todos* os tipos podem `derive` (criar automaticamente) a implementação `fmt::Debug`. Isto não é verdadeiro para `fmt::Display` que deve ser implementada manualmente:

```rust
// Esta estrutura não pode ser impressa nem com `fmt::Display` ou
// com `fmt::Debug`.
struct UnPrintable(i32);

// O atributo `derive` cria automaticamente a implementação exigida
// para tornar esta `struct` imprimível com `fmt::Debug`.
#[derive(Debug)]
struct DebugPrintable(i32);
```

Todos os tipos da biblioteca `std` são automaticamente imprimíveis também com `{:?}`:

```rust,editable
// Derivar a implementação `fmt::Debug` para `Structure`.
// `Structure` é uma estrutura que contém um único `i32`.
#[derive(Debug)]
struct Structure(i32);

// Colocar uma `Structure` dentro da estrutura `Deep`.
// Também a torna imprimível.
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // Imprimir com `{:?}` é semelhante à com `{}`.
    println!("{:?} months in a year.", 12);
    println!("{1:?} {0:?} is the {actor:?} name.",
             "Slater",
             "Christian",
             actor="actor's");

    // `Structure` é imprimível!
    println!("Now {:?} will print!", Structure(3));

    // O problema com `derive` é que não existe controlo sobre
    // a aparência do resultado. E se quisermos que isto só mostre um `7`?
    println!("Now {:?} will print!", Deep(Structure(7)));
}
```

Assim `fmt::Debug` definitivamente torna isto imprimível mas sacrifica alguma elegância. A Rust também fornece "impressão elegante" com `{:#?}`:

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // Imprimir com elegância
    println!("{:#?}", peter);
}
```

Um pode manualmente implementar `fmt::Display` para controlar a exibição.

### Consulte também:

[`attributes`][attributes], [`derive`][derive], [`std::fmt`][fmt],
e [`struct`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md


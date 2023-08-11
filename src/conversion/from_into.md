# `From` e `Into`

As características [`From`] e [`Into`] estão inerentemente ligadas, e isto é efetivamente parte da sua implementação. Se fores capaz de converter o tipo A a partir do tipo B, então deveria ser fácil acreditar que deveríamos ser capaz de converter o tipo B para o tipo A.

## `From`

A característica [`From`] permite um tipo definir como criar-se a partir doutro tipo, daí fornecendo um mecanismo muito simples para converter entre vários tipos. Existem numerosas implementações desta característica dentro da biblioteca padrão para conversão de tipos primitivos e comuns.

Por exemplo podemos facilmente converter uma `str` numa `String`:

```rust
let my_str = "hello";
let my_string = String::from(my_str);
```

Nós podemos fazer algo semelhante para definir uma conversão para o nosso próprio tipo.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let num = Number::from(30);
    println!("My number is {:?}", num);
}
```

## `Into`

A característica [`Into`] é simplesmente o recíproco da característica `From`. Isto é, se tiveres implementado a característica `From` para o teu tipo, `Into` o chamará quando necessário.

O uso da característica `Into` normalmente exigirá especificação do tipo para converter conforme o compilador for incapaz de determinar isto na maioria das vezes. No entanto, isto é um pequeno compromisso considerando que recebemos a funcionalidade gratuitamente:

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let int = 5;
    // Tente remover a anotação de tipo
    let num: Number = int.into();
    println!("My number is {:?}", num);
}
```

[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html

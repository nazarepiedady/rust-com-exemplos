# `if let`

Para alguns casos de uso, quando correspondemos enumerações, `match` é difícil. Por exemplo:

```rust
// Tornar `optional` do tipo `Option<i32>`
let optional = Some(7);

match optional {
    Some(i) => {
        println!("This is a really long string and `{:?}`", i);
        // ^ Precisava de 2 indentações só assim poderíamos 
        // desestruturar `i` a partir da opção.
    },
    _ => {},
    // ^ Obrigatório porque `match` é exaustiva.
    // Não parece como espaço desperdiçado?
};

```

`if let` é mais clara para este caso de uso e além disso permite várias opções de fracasso a serem especificadas:

```rust,editable
fn main() {
    // Todos têm o tipo `Option<i32>`
    let number = Some(7);
    let letter: Option<i32> = None;
    let emoticon: Option<i32> = None;

    // A construção `if let` lê-se: "se `let` desestruturar `number` na"
    // `Some(i)`, avaliar o bloco (`{}`).
    if let Some(i) = number {
        println!("Matched {:?}!", i);
    }

    // Se precisarmos de especificar uma falha, usamos uma `else`:
    if let Some(i) = letter {
        println!("Matched {:?}!", i);
    } else {
        // Desestruturação falhada. Mudar para o caso de falha.
        println!("Didn't match a number. Let's go with a letter!");
    }

    // Fornecer uma condição de falha alterada.
    let i_like_letters = false;

    if let Some(i) = emoticon {
        println!("Matched {:?}!", i);
    // Desestruturação falhada. Avaliar uma condição `else if` para
    // ver se o ramo de falha alternada deveria ser considerado:
    } else if i_like_letters {
        println!("Didn't match a number. Let's go with a letter!");
    } else {
        // A condição avaliou `false`. Este ramo é o padrão:
        println!("I don't like letters. Let's go with an emoticon :)!");
    }
}
```

De algum modo, `if let` pode ser usada para corresponder apenas o valor de enumeração:

```rust,editable
// Nossa enumeração de exemplo
enum Foo {
    Bar,
    Baz,
    Qux(u32)
}

fn main() {
    // Criar variáveis de exemplo
    let a = Foo::Bar;
    let b = Foo::Baz;
    let c = Foo::Qux(100);
    
    // Variável `a` corresponde `Foo::Bar`
    if let Foo::Bar = a {
        println!("a is foobar");
    }
    
    // Variável `b` não corresponde `Foo::Bar`
    // Então isto não imprimirá nada
    if let Foo::Bar = b {
        println!("b is foobar");
    }
    
    // Variável `c` corresponde `Foo::Qux` que tem um valor
    // Semelhante à `Some()` no exemplo anterior
    if let Foo::Qux(value) = c {
        println!("c is {}", value);
    }

    // Vínculos também funcionam com `if let`
    if let Foo::Qux(value @ 100) = c {
        println!("c is one hundred");
    }
}
```

Um outro beneficio é que `if let` permite-nos corresponder variantes de enumeração não parametrizadas. Isto é verdadeiro mesmo em casos onde a enumeração não implementa ou deriva `PartialEq`. Em tais casos `if Foo::Bar == a` falharia ao compilar, porque as instâncias da enumeração não podem ser equiparadas, no entanto `if let` continuará a funcionar.

Gostarias dum desafio? Corrija o seguinte exemplo para usar `if let`:

```rust,editable,ignore,mdbook-runnable
// Esta enumeração propositadamente não implemente nem deriva `PartialEq`.
// É por isto que a comparação abaixo `Foo::Bar == a` falha.
enum Foo {Bar}

fn main() {
    let a = Foo::Bar;

    // Variável `a` corresponde `Foo::Bar`
    if Foo::Bar == a {
    // ^-- isto causa um erro de tempo de compilação. Use `if let`.
        println!("a is foobar");
    }
}
```

### Consulte também:

[`enum`][enum], [`Option`][option], e o [RFC][if_let_rfc]

[enum]: ../custom_types/enum.md
[if_let_rfc]: https://github.com/rust-lang/rfcs/pull/160
[option]: ../std/option.md

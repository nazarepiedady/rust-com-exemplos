# Laços de Repetição `for`

## `for` e o limite

A construção `for in` pode ser usada para iterar através dum `Iterator`. Uma das maneiras mais fáceis de criar um iterador é usar a notação de limite `a..b`. Isto produz valores a partir de `a` (inclusivo) à `b` (exclusivo) em passos de um.

Vamos escrever FizzBuzz usando `for` ao invés de `while`.

```rust,editable
fn main() {
    // `n` receberá os valores: 1, 2, ..., 100 em cada iteração
    for n in 1..101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

Alternativamente, `a..=b` pode ser usado para um limite que é inclusivo em ambos fins. O exemplo acima pode ser escrito como:

```rust,editable
fn main() {
    // `n` receberá os valores: 1, 2, ..., 100 em cada iteração
    for n in 1..=100 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

## `for` e os iteradores

A construção `for in` é capaz de interagir com um `Iterator` de muitas maneiras. Conforme discutido na seção sobre a característica [`Iterator`][iter], por padrão o laço `for` aplicará a função `into_iter` à coleção. No entanto, isto não é o único significado de converter coleções em iteradores.

`into_iter`, `iter` e `iter_mut` manipulam a conversão duma coleção num iterador de maneiras diferentes, fornecendo visões diferentes sobre os dados no interior.

* `iter` - Este pedi emprestado cada elemento da coleção durante cada iteração. Assim deixando a coleção intocada e disponível para reuso depois do laço.

```rust,editable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter() {
        match name {
            &"Ferris" => println!("There is a rustacean among us!"),
            // TODO ^ Tente eliminar o & e corresponder apenas "Ferris"
            _ => println!("Hello {}", name),
        }
    }
    
    println!("names: {:?}", names);
}
```

* `into_iter` - Este consume a coleção para que em cada iteração o dado exato ser fornecido. Assim que a coleção tiver sido consumida não estará disponível para reuso como se tivesse sido 'movida' dentro do laço.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.into_iter() {
        match name {
            "Ferris" => println!("There is a rustacean among us!"),
            _ => println!("Hello {}", name),
        }
    }
    
    println!("names: {:?}", names);
    // FIXME ^ Comente esta linha
}
```

* `iter_mut` - Este pedi emprestado de maneira mutável cada elemento da coleção, permitindo a coleção ser modificada no lugar.

```rust,editable
fn main() {
    let mut names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter_mut() {
        *name = match name {
            &mut "Ferris" => "There is a rustacean among us!",
            _ => "Hello",
        }
    }

    println!("names: {:?}", names);
}
```

Nos trechos acima nota o tipo do ramo `match`, que é a diferença chave nos tipos de iteração. A diferença no tipo portanto com certeza implica que diferentes ações que são capazes de ser realizadas.

### Consulte também:

[Iterator][iter]

[iter]: ../trait/iter.md

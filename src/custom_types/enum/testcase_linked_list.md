# Caso de Teste: Lista Ligada

Um maneira comum de implementar uma lista ligada é através de `enums`:

```rust,editable
use crate::List::*;

enum List {
    // Cons: estrutura de tipo que envolve um elemento e 
    // um ponteiro para o próximo nó.
    Cons(u32, Box<List>),
    // Nil: Um nó que significa o fim da lista ligada
    Nil,
}

// Os métodos podem ser anexados à numa enumeração
impl List {
    // Criar uma lista vazia
    fn new() -> List {
        // `Nil` tem o tipo `List`
        Nil
    }

    // Consumir uma lista, e retornar a mesma lista com
    // um novo elemento na sua frente
    fn prepend(self, elem: u32) -> List {
        // `Cons` também tem o tipo `List`
        Cons(elem, Box::new(self))
    }

    // Retornar o comprimento da lista
    fn len(&self) -> u32 {
        // `self` precisa ser correspondido, porque o comportamento deste método
        // depende da variante do `self`.
        // `self` tem o tipo `&List`, e `*self` tem o tipo `List`,
        // correspondência dum tipo concreto `T` é preferida sobre 
        // uma correspondência numa referência `&T`, depois da Rust 2018 
        // podes usar `self` aqui e também perseguir (sem referência) abaixo,
        // Rust inferirá `&s` e referenciará a cauda.
        // See https://doc.rust-lang.org/edition-guide/rust-2018/ownership-and-lifetimes/default-match-bindings.html
        match *self {
            // Não possível tomar posse da cauda, porque `self` é emprestado;
            // ao invés disto recebe uma referência à cauda
            Cons(_, ref tail) => 1 + tail.len(),
            // Caso de Base: Uma lista vaziam tem comprimento zero
            Nil => 0
        }
    }

    // Retornar a representação da lista como uma
    // sequência de caracteres (monte alocado)
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!` é semelhante à `print!`, mas retorna uma
                // sequência de caracteres de monte alocado de impressão
                // para a consola.
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // Criar uma lista ligada vazia
    let mut list = List::new();

    // Adicionar ao começo da lista alguns elementos
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // Mostrar o estado final da lista
    println!("linked list has length: {}", list.len());
    println!("{}", list.stringify());
}
```

### Consulte também:

[`Box`][box] e [métodos][methods]

[box]: ../../std/box.md
[methods]: ../../fn/methods.md

# Caso de Teste: Lista

Implementar `fmt::Display` para uma estrutura onde os elementos devem cada um ser manipulados sequencialmente é complicado. O problema é que cada `write!` gera um `fmt::Result`. A manipulação apropriada disto exige lidar com *todos* os resultados. A Rust fornece o operador `?` para exatamente este propósito.

Usar `?` na `write!` parece-se com isto:

```rust,ignore
// Tentar `write!` para ver se erra. Se errar, retorne o erro.
// De outro modo continue.
write!(f, "{}", value)?;
```

Com `?` disponível, implementar `fmt::Display` para uma `Vec` é simples:

```rust,editable
use std::fmt; // Importar o módulo `fmt`.

// Definir uma estrutura nomeada `List` contendo uma `Vec`.
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Extrair o valor usando a indexação de tupla,
        // e criar uma referência para `vec`.
        let vec = &self.0;

        write!(f, "[")?;

        // Iterar sobre `v` em `vec` enquanto enumera a 
        // contagem da iteração em `count`.
        for (count, v) in vec.iter().enumerate() {
            // Para cada elemento exceto o primeiro, adicione uma vírgula.
            // Usar o operador `?` para retornar em erros.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // Fechar o parênteses retos e retornar um valor de `fmt::Result`
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```

### Atividade

Tente mudar o programa para que o índice de cada elemento no vetor seja também imprimido. A nova saída deveriam parecer-se com isto:

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

### Consulte também:

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`?`][q_mark], e [`vec!`][vec]

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md

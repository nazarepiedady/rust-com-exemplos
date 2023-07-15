# `use`

A declaração `use` pode ser usado então a delimitação do âmbito não é necessária:

```rust,editable
// Um atributo para esconder avisos de código não usado.
#![allow(dead_code)]

enum Status {
    Rich,
    Poor,
}

enum Work {
    Civilian,
    Soldier,
}

fn main() {
    // Usar explicitamente cada nome assim estão disponíveis
    // sem a delimitação manual.
    use crate::Status::{Poor, Rich};
    // Usar automaticamente cada nome dentro de `Work`.
    use crate::Work::*;

    // Equivalente ao `Status::Poor`.
    let status = Poor;
    // Equivalente ao `Work::Civilian`.
    let work = Civilian;

    match status {
        // Nota a falta de delimitação de âmbito por causa do
        // uso explícito acima.
        Rich => println!("The rich have lots of money!"),
        Poor => println!("The poor have no money..."),
    }

    match work {
        // Nota novamente a falte de delimitação do âmbito.
        Civilian => println!("Civilians work!"),
        Soldier  => println!("Soldiers fight!"),
    }
}
```

### Consulte também:

[`match`][match] e [`use`][use] 

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md

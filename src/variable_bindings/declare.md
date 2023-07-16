# Declarar primeiro

É possível declarar vínculos de variável primeiro, e inicializa-los depois. No entanto, esta forma é raramente usada, visto que pode conduzir à uso de variáveis não inicializadas.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // Declarar um vínculo de variável
    let a_binding;

    {
        let x = 2;

        // Inicializar o vínculo
        a_binding = x * x;
    }

    println!("a binding: {}", a_binding);

    let another_binding;

    // Erro! Uso de vínculo não inicializado
    println!("another binding: {}", another_binding);
    // FIXME ^ Comenta esta linha

    another_binding = 1;

    println!("another binding: {}", another_binding);
}
```

O compilador proíbe o uso de variáveis não inicializadas, visto que isto conduziria à comportamento não definido.

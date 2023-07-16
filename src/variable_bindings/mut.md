# Mutabilidade

Os vínculos de variável são imutáveis por padrão, mas isto pode ser sobreposto usando o modificador `mut`.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let _immutable_binding = 1;
    let mut mutable_binding = 1;

    println!("Before mutation: {}", mutable_binding);

    // Ok
    mutable_binding += 1;

    println!("After mutation: {}", mutable_binding);

    // Erro! Não é possível atribuir um novo valor à uma variável imutável
    _immutable_binding += 1;
}
```

O compilador lançará um diagnóstico detalhado sobre os erros de mutabilidade.

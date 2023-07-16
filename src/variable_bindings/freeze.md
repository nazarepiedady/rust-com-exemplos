# Congelação

Quando o dado estiver vinculado ao mesmo nome imutavelmente, ele também *congela*. O dado *congelado* não pode ser modificado até o vínculo imutável sair do âmbito:

```rust,editable,ignore,mdbook-runnable
fn main() {
    let mut _mutable_integer = 7i32;

    {
        // Obscurecimento pela `_mutable_integer` imutável
        let _mutable_integer = _mutable_integer;

        // Erro! `_mutable_integer` está congelado neste âmbito
        _mutable_integer = 50;
        // FIXME ^ Comente esta linha

        // `_mutable_integer` sai fora do âmbito
    }

    // Ok! `_mutable_integer` não está congelado neste âmbito
    _mutable_integer = 3;
}
```

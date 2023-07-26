# Inferência

O motor da inferência de tipo é muito inteligente. Ele faz mais do que olhar o tipo da expressão do valor durante uma inicialização. Ele também olha em como a variável é usado mais tarde para inferir o seu tipo. Cá está um exemplo avançado da inferência de tipo:

```rust,editable
fn main() {
    // Por causa da anotação, o compilador sabe que `elem` tem o tipo u8.
    let elem = 5u8;

    // Criar um vetor vazio (uma tabela que cresce).
    let mut vec = Vec::new();
    // Neste momento o compilador não sabe o tipo exato de `vec`,
    // apenas sabe que é um vetor de alguma coisa (`Vec<_>`).

    // Inserir `elem` no vetor.
    vec.push(elem);
    // Aha! Agora o compilador sabe que `vec` é um vetor de `u8` (`Vec<u8>`)
    // TODO ^ Tente comentar a linha `vec.push(elem)`

    println!("{:?}", vec);
}
```

Nenhuma anotação de tipo de variáveis foi necessária, o compilador está feliz e consequentemente o programador!

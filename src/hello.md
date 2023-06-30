# Olá Mundo

Este é o código-fonte do programa "Hello World" tradicional:

```rust,editable
// Isto é um comentário, e é ignorado pelo compilador.
// Podemos testar este código clicando o botão "Run" ou
// se preferirmos usar o nosso teclado, podemos usar o atalho "Ctrl + Enter"

// Este código é editável, sinta-se a vontade para alterá-lo!
// Podemos sempre retornar para o código original clicando o botão "Reset" ->

// Esta é a função principal.
fn main() {
    // Declarações nesta função são executadas quando o binário for chamado.

    // Imprime o texto na consola.
    println!("Hello World!");
}
```

`println!` é uma [*macro*][macros] que imprime o texto na consola.

Um binário pode ser gerado usando o compilador da Rust: `rustc`:

```bash
$ rustc hello.rs
```

`rustc` produzirá um binário `hello` que pode ser executado:

```bash
$ ./hello
Hello World!
```

### Atividade

Clique sobre o 'Run' acima para veres a saída esperada. Depois, adicione uma nova linha com uma segunda macro `println!` para que a saída exiba:

```text
Hello World!
I'm a Rustacean!
```

[macros]: macros.md

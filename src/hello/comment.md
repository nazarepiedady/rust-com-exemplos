# Comentários

Qualquer programa requer comentários, e a Rust suporta algumas variedades diferentes:

* *Comentários normais* que são ignorados pelo compilador:
  * `// Comentários de linha que vão até ao final da linha.`
  * `/* Comentários de bloco que vão até o delimitador de fechamento. */`
* *Comentários de documentação* que são analisados para [documentação][docs] da biblioteca em HTML:
  * `/// Gera documentações da biblioteca para o seguinte item.`
  * `//! Gera as documentações da biblioteca para o item de fechamento.`

```rust,editable
fn main() {
    // Isto é um exemplo de comentário duma linha.
    // Existem duas barras no princípio da linha.
    // E nada escrito depois destas será lido pelo compilador.

    // println!("Hello, world!");

    // Execute-o. Vês? Agora tente eliminar as duas barras, e execute-o novamente.

    /*
     * Isto é um outro tipo de comentário, um bloco de comentário. Em geral,
     * comentários de linha são o estilo de comentário recomendado.
     * Mas os comentários de bloco são extremamente úteis para
     * desativar temporariamente pedaços de código.
     * /* Comentários de bloco podem ser /* encaixados, */ */ então apenas custa
     * alguns toques na tecla para comentar tudo nesta função `main()`.
     * /*/*/* Experimente-o tu mesmo! */*/*/
     */

    /*
    Nota: a anterior coluna de `*` foi inteiramente para estilo. Não existe
    de fato necessidade disto.
    */

    // Nós podemos manipular as expressões mais facilmente com comentários
    // de bloco do que com comentários de linha.
    // Tente eliminar os delimitadores de comentário para mudar o resultado:
    let x = 5 + /* 90 + */ 5;
    println!("Is `x` 10 or 100? x = {}", x);
}
```

### Consulte também:

[Documentação de biblioteca][docs]

[docs]: ../meta/doc.md

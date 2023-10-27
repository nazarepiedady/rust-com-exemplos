# Vetores e Pedaços

Um vetor é uma coleção de objetos do mesmo tipo `T`, armazenados na memória contígua. Os vetores são criados usando parênteses retos `[]`, e o seu comprimento, que é conhecido em tempo de compilação, é parte da sua assinatura de tipo `[T; length]`.

Os pedaços são semelhantes aos vetores, mas seu comprimento não é conhecido em tempo de compilação. Ao invés disto, um pedaço é um objeto de duas palavras; a primeira palavra é um ponteiro para o dado, e a segunda palavra o comprimento do pedaço. O tamanho da palavra é o mesmo que não ter tamanho `usize`, determinado pela arquitetura do processador, por exemplo, 64 bits numa x86-64. Os pedaços podem ser usados para pedir emprestado uma seção dum vetor e têm a assinatura de tipo `&[T]`:

```rust,editable,ignore,mdbook-runnable
use std::mem;

// Esta função pedi emprestado um pedaço.
fn analyze_slice(slice: &[i32]) {
    println!("First element of the slice: {}", slice[0]);
    println!("The slice has {} elements", slice.len());
}

fn main() {
    // Vetor de tamanho fixo (assinatura de tipo é supérflua).
    let xs: [i32; 5] = [1, 2, 3, 4, 5];

    // Todos os elementos podem ser inicializados para o mesmo valor.
    let ys: [i32; 500] = [0; 500];

    // A indexação começa em 0.
    println!("First element of the array: {}", xs[0]);
    println!("Second element of the array: {}", xs[1]);

    // `len` retorna a contagem de elementos no vetor.
    println!("Number of elements in array: {}", xs.len());

    // Os vetores são pilhas alocadas.
    println!("Array occupies {} bytes", mem::size_of_val(&xs));

    // Os vetores podem ser pedidos emprestado como pedaços.
    println!("Borrow the whole array as a slice.");
    analyze_slice(&xs);

    // Os pedaços podem apontar para uma seção dum vetor.
    // Eles são da forma [starting_index..ending_index].
    // `starting_index` é a primeira posição no pedaço.
    // `ending_index` é a última posição no pedaço.
    println!("Borrow a section of the array as a slice.");
    analyze_slice(&ys[1 .. 4]);

    // Exemplo de pedaço vazio `&[]`:
    let empty_array: [u32; 0] = [];
    assert_eq!(&empty_array, &[]);
    assert_eq!(&empty_array, &[][..]); // O mesmo mas mais verboso

    // Os vetores podem ser acessados seguramente usando `.get`, que retorna
    // uma `Option`. Isto pode ser correspondido como mostrado abaixo, ou usado
    // com `.expect()` se gostarias que o programa saísse com uma mensagem
    // agradável ao invés de felizmente continuar.
    for i in 0..xs.len() + 1 { // Oops, um elemento longe de mais!
        match xs.get(i) {
            Some(xval) => println!("{}: {}", i, xval),
            None => println!("Slow down! {} is too far!", i),
        }
    }

    // Indexação fora do limite no vetor causa erro de tempo de compilação.
    //println!("{}", xs[5]);
    // // Indexação fora do limite no pedaço causa erro de tempo de execução.
    //println!("{}", xs[..][5]);
}
```

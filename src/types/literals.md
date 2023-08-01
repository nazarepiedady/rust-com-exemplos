# Literais

Os literais numéricos podem ser anotados por tipo adicionado o tipo como um sufixo. Como um exemplo, para especificar que o literal `42` deveria ter o tipo `i32`, escreva `42i32`.

O tipo dos literais numéricos sem sufixo depende de como são usados. Se não existir nenhuma restrição, o compilador usará `i32` para os inteiros, e `f64` para os números de ponto flutuante.

```rust,editable
fn main() {
    // Literais com sufixo, seus tipos são conhecidos na inicialização
    let x = 1u8;
    let y = 2u32;
    let z = 3f32;

    // Literais sem sufixo, seus tipos dependem de como são usados
    let i = 1;
    let f = 1.0;

    // `size_of_val` retorna o tamanho duma variável em bytes
    println!("size of `x` in bytes: {}", std::mem::size_of_val(&x));
    println!("size of `y` in bytes: {}", std::mem::size_of_val(&y));
    println!("size of `z` in bytes: {}", std::mem::size_of_val(&z));
    println!("size of `i` in bytes: {}", std::mem::size_of_val(&i));
    println!("size of `f` in bytes: {}", std::mem::size_of_val(&f));
}
```

Existem alguns conceitos usados no código anterior que ainda não foram explicados, cá está uma breve explicação para os leitores impacientes:

* `std::mem::size_of_val` é uma função, mas chamada com o seu *caminho completo*. O código pode ser separado em unidades lógicas chamadas de *módulos*. Neste caso, a função `size_of_val` é definida no módulo `mem`, e o módulo `mem` é definida no *caixote* `std`. Para mais detalhes, consulte os [módulos][mod] e [caixotes][crate].

[mod]: ../mod.md
[crate]: ../crates.md

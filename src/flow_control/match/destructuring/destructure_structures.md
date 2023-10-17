# Estruturas

De maneira semelhante, uma `struct` pode ser desestruturada como mostrada:

```rust,editable
fn main() {
    struct Foo {
        x: (u32, u32),
        y: u32,
    }

    // Experimente mudar os valores na estrutura para veres o que acontece
    let foo = Foo { x: (1, 2), y: 3 };

    match foo {
        Foo { x: (1, b), y } => println!("First of x is 1, b = {},  y = {} ", b, y),

        // nós podemos desestruturar as estruturas e renomear as variáveis,
        // a ordem não é importante
        Foo { y: 2, x: i } => println!("y is 2, i = {:?}", i),

        // e também podemos ignorar algumas variáveis:
        Foo { y, .. } => println!("y = {}, we don't care about x", y),
        // isto dará um erro: o padrão não menciona o campo `x`
        //Foo { y } => println!("y = {}", y),
    }

    let faa = Foo { x: (1, 2), y: 3 };

    // Nós não precisamos dum bloco de correspondência para
    // desestruturar as estruturas:
    let Foo { x : x0, y: y0 } = faa;
    println!("Outside: x0 = {x0:?}, y0 = {y0}");
}
```

### Consulte também:

[Estruturas](../../../custom_types/structs.md)

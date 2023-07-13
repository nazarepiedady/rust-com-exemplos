# Estruturas

Existem três tipos de estruturas ("structs") que podem ser criadas usando a palavra-chave `struct`:

* Estruturas de tupla, que são, basicamente, tuplas nomeadas.
* A [estruturas de C][c_struct] clássicas,
* Estruturas unitárias, que são sem campo, são úteis para genéricos.

```rust,editable
// Um atributo para esconder avisos de código não usado.
#![allow(dead_code)]

#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

// Uma estrutura unitária
struct Unit;

// Um estrutura de tupla
struct Pair(i32, f32);

// Uma estrutura com dois campos
struct Point {
    x: f32,
    y: f32,
}

// As estruturas podem ser reutilizadas como campos duma outra estrutura
struct Rectangle {
    // Um retângulo pode ser especificado pela posição dos cantos
    // superior esquerdo e inferior direito no espaço.
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // Criar a estrutura com a abreviatura de inicialização de campo
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };

    // Imprimir em depuração a estrutura
    println!("{:?}", peter);

    // Instanciar um `Point`
    let point: Point = Point { x: 10.3, y: 0.4 };

    // Acessar os campos do ponto
    println!("point coordinates: ({}, {})", point.x, point.y);

    // Criar um novo ponto usando a sintaxe de atualização de estrutura
    // para usar os campos do nosso outro
    let bottom_right = Point { x: 5.2, ..point };

    // `bottom_right.y` será o mesmo que `point.y` porque usamos este campo
    // a partir de `point`
    println!("second point: ({}, {})", bottom_right.x, bottom_right.y);

    // Desestruturar o ponto usando uma vínculo `let`
    let Point { x: left_edge, y: top_edge } = point;

    let _rectangle = Rectangle {
        // A instanciação da estrutura também é uma expressão
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };

    // Instanciar uma estrutura unitária
    let _unit = Unit;

    // Instanciar uma estrutura de tupla
    let pair = Pair(1, 0.1);

    // Acessar os campos duma estrutura de tupla
    println!("pair contains {:?} and {:?}", pair.0, pair.1);

    // Desestruturar uma estrutura de tupla
    let Pair(integer, decimal) = pair;

    println!("pair contains {:?} and {:?}", integer, decimal);
}
```

### Atividade

1. Adicione uma função `rect_area` que calcula a área dum `Rectangle` (tente usar desestruturação encaixada).
2. Adicione uma função `square` que recebe um `Point` e um `f32` como argumentos, e retorna um `Rectangle` com o seu canto superior esquerdo no ponto, e uma largura e altura correspondendo ao `f32`.

### Consulte também

[`attributes`][attributes], e [desestruturação][destructuring]

[attributes]: ../attribute.md
[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md

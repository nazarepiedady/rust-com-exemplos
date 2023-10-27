# Tuplas

Uma tupla é uma coleção de valores de tipos diferentes. As tuplas são construídas usando parênteses `()` e cada tupla por si mesma é um valor com a assinatura de tipo `(T1, T2, ...)`, onde `T1`, `T2` são os tipos dos seus membros. As funções podem usar tuplas para retornarem vários valores, visto que as tuplas podem segurar qualquer número de valores:

```rust,editable
// As tuplas podem ser usadas como argumentos de função e retornar valores.
fn reverse(pair: (i32, bool)) -> (bool, i32) {
    // `let` pode ser usado para vincular os membros duma tupla às variáveis.
    let (int_param, bool_param) = pair;

    (bool_param, int_param)
}

// A seguinte estrutura é para a atividade.
#[derive(Debug)]
struct Matrix(f32, f32, f32, f32);

fn main() {
    // Uma tupla com um grupo de tipos diferentes.
    let long_tuple = (1u8, 2u16, 3u32, 4u64,
                      -1i8, -2i16, -3i32, -4i64,
                      0.1f32, 0.2f64,
                      'a', true);

    // Os valores podem ser extraídos da tupla usando indexação de tupla.
    println!("Long tuple first value: {}", long_tuple.0);
    println!("Long tuple second value: {}", long_tuple.1);

    // As tuplas podem ser membros de tupla.
    let tuple_of_tuples = ((1u8, 2u16, 2u32), (4u64, -1i8), -2i16);

    // As tuplas são imprimíveis.
    println!("tuple of tuples: {:?}", tuple_of_tuples);

    // Mas tuplas longas (mas de 12 elementos) não podem ser imprimidas.
    //let too_long_tuple = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13);
    //println!("Too long tuple: {:?}", too_long_tuple);
    // TODO ^ Tente desfazer o comentário das 2 linhas acima
    // para veres o erro do compilador

    let pair = (1, true);
    println!("Pair is {:?}", pair);

    println!("The reversed pair is {:?}", reverse(pair));

    // Para criar tuplas de um elemento, a vírgula é obrigatória para
    // distingui-las dum literal envolvido por parênteses.
    println!("One element tuple: {:?}", (5u32,));
    println!("Just an integer: {:?}", (5u32));

    // As tuplas podem ser desconstruídas para criar vínculos.
    let tuple = (1, "hello", 4.5, true);

    let (a, b, c, d) = tuple;
    println!("{:?}, {:?}, {:?}, {:?}", a, b, c, d);

    let matrix = Matrix(1.1, 1.2, 2.1, 2.2);
    println!("{:?}", matrix);
}
```

### Atividade

2. *Recapitulação*: Adicione a característica `fmt::Display` à estrutura `Matrix` no exemplo acima, para que se mudares da impressão do formato de depuração `{:?}` para o formato de exibição `{}`, consigas ver a seguinte saída:

   ```text
   ( 1.1 1.2 )
   ( 2.1 2.2 )
   ```

   Podemos consultar o exemplo para [impressão de exibição][print_display].
2. Adicione uma função `transpose` usando a função `reverse` como molde, que aceita uma matriz como argumento, e retorna uma matriz na qual dos elementos têm sido trocados. Por exemplo:

   ```rust,ignore
   println!("Matrix:\n{}", matrix);
   println!("Transpose:\n{}", transpose(matrix));
   ```

   Resulta na saída:

   ```text
   Matrix:
   ( 1.1 1.2 )
   ( 2.1 2.2 )
   Transpose:
   ( 1.1 2.1 )
   ( 1.2 2.2 )
   ```

[print_display]: ../hello/print/print_display.md

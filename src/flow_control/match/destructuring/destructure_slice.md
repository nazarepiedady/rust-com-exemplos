# Vetores ou Pedaços

Tal como as tuplas, os vetores e pedaços podem ser desestruturados desta maneira:

```rust,editable
fn main() {
    // Experimente mudar os valores no vetor, ou torne-o num pedaço!
    let array = [1, -2, 6];

    match array {
        // Vincula o segundo e o terceiro elemento às respetivas variáveis
        [0, second, third] =>
            println!("array[0] = 0, array[1] = {}, array[2] = {}", second, third),

        // Os valores individuais podem ser ignorados com _
        [1, _, third] => println!(
            "array[0] = 1, array[2] = {} and array[1] was ignored",
            third
        ),

        // Nós também podemos vincular alguns e ignorar o resto
        [-1, second, ..] => println!(
            "array[0] = -1, array[1] = {} and all the other ones were ignored",
            second
        ),
        // O código abaixo não compilaria
        // [-1, second] => ...

        // Ou armazena-os noutro vetor ou pedaço (o tipo depende do
        // valor que está sendo comparado)
        [3, second, tail @ ..] => println!(
            "array[0] = 3, array[1] = {} and the other elements were {:?}",
            second, tail
        ),

        // Combinado estes padrões, podemos, por exemplo, vincular os
        // primeiros e últimos valores, e armazenar o resto deles num único vetor
        [first, middle @ .., last] => println!(
            "array[0] = {}, middle = {:?}, array[2] = {}",
            first, middle, last
        ),
    }
}
```

### Consulte também:

[Vetores e Pedaços](../../../primitives/array.md) e [Vínculo](../binding.md) pelo símbolo `@`

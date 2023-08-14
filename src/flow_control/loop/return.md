# Regressar dos Laços de Repetições

Um dos usos dum `loop` é para voltar a tentar uma operação até ser bem-sucedida. Mas se a operação retornar um valor, podes precisar de passá-lo ao resto do código: colocá-lo depois da `break`, e será retornado pela expressão `loop`.

```rust,editable
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    assert_eq!(result, 20);
}
```

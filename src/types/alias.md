# Pseudónimos

A declaração `type` pode ser usada para dar um novo nome à um tipo existente. Os tipos devem ter nomes com o seguinte padrão `UpperCamelCase`, ou o compilador levantará um aviso.  As exceções à esta regra são os tipos primitivos: `usize`, `f32`, etc.

```rust,editable
// `NanoSecond`, `Inch`, e `U64` são novos nomes para `u64`.
type NanoSecond = u64;
type Inch = u64;
type U64 = u64;

fn main() {
    // `NanoSecond` = `Inch` = `U64` = `u64`.
    let nanoseconds: NanoSecond = 5 as U64;
    let inches: Inch = 2 as U64;

    // Nota que os pseudónimos de tipo *não* fornecem qualquer segurança de
    // tipo adicional, porque os pseudónimos *não* são novos tipos
    println!("{} nanoseconds + {} inches = {} unit?",
             nanoseconds,
             inches,
             nanoseconds + inches);
}
```

O uso principal de pseudónimos é reduzir a complexidade; por exemplo o tipo `io::Result<T>` é um pseudónimo para o tipo `Result<T, io::Error>`.

### Consulte também:

[Atributos](../attribute.md)

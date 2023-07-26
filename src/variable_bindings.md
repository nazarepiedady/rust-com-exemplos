# Vínculos de Variável

A Rust fornece segurança de tipo através da definição de tipos estáticos. Os vínculos de variável pode ter o seu tipo anotado quando declarados. No entanto, na maioria dos casos, o compilador será capaz de inferir o tipo da variável a partir do contexto, reduzindo grandemente o fardo da anotação.

Os valores (tais como literais) podem ser vinculados às variáveis, usando o vínculo de `let`.

```rust,editable
fn main() {
    let an_integer = 1u32;
    let a_boolean = true;
    let unit = ();

    // copiar `an_integer` para `copied_integer`
    let copied_integer = an_integer;

    println!("An integer: {:?}", copied_integer);
    println!("A boolean: {:?}", a_boolean);
    println!("Meet the unit value: {:?}", unit);

    // O compilador avisa sobre vínculos de variáveis não usados;
    // estes avisos podem ser silenciados prefixando o nome da variável
    // com um sublinhado.
    let _unused_variable = 3u32;

    let noisy_unused_variable = 2u32;
    // FIXME ^ Prefixe com um sublinhado para suprimir o aviso
    // Nota que os avisos podem não ser exibidos num navegador
```

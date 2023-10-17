# Enumerações

Uma `enum` é desestruturada de maneira semelhante:

```rust,editable
// `allow` exigido para silenciar os avisos
// porque apenas uma variante é usada.
#[allow(dead_code)]
enum Color {
    // Estes 3 são especificados unicamente pelo seu nome.
    Red,
    Blue,
    Green,
    // Estes igualmente atam as tuplas de `u32` para
    // nomes diferentes: modelos de cor.
    RGB(u32, u32, u32),
    HSV(u32, u32, u32),
    HSL(u32, u32, u32),
    CMY(u32, u32, u32),
    CMYK(u32, u32, u32, u32),
}

fn main() {
    let color = Color::RGB(122, 17, 40);
    // TODO ^ Experimente diferentes variantes para `color`

    println!("What color is it?");
    // Uma `enum` pode ser desestruturada usando uma `match`.
    match color {
        Color::Red   => println!("The color is Red!"),
        Color::Blue  => println!("The color is Blue!"),
        Color::Green => println!("The color is Green!"),
        Color::RGB(r, g, b) =>
            println!("Red: {}, green: {}, and blue: {}!", r, g, b),
        Color::HSV(h, s, v) =>
            println!("Hue: {}, saturation: {}, value: {}!", h, s, v),
        Color::HSL(h, s, l) =>
            println!("Hue: {}, saturation: {}, lightness: {}!", h, s, l),
        Color::CMY(c, m, y) =>
            println!("Cyan: {}, magenta: {}, yellow: {}!", c, m, y),
        Color::CMYK(c, m, y, k) =>
            println!("Cyan: {}, magenta: {}, yellow: {}, key (black): {}!",
                c, m, y, k),
        // Não precisa doutro braço porque todas variantes foram examinadas
    }
}
```

### Consulte também:

[`#[allow(...)]`][allow], [modelos de cor][color_models] e [`enum`][enum]

[allow]: ../../../attribute/unused.md
[color_models]: https://en.wikipedia.org/wiki/Color_model
[enum]: ../../../custom_types/enum.md

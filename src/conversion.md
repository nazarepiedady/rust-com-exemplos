# Conversão

Os tipos primitivos podem ser convertidos à um ao outro através da [moldagem][casting].

A Rust aborda a conversão entre tipos personalizados (por exemplo, `struct` e `enum`) com o uso de [características][traits]. As conversões genéricas usarão as características [`From`] e [`Into`]. No entanto existem aquelas mais específicas para casos mais comuns, em especial quando convertemos para e de `String`.

[casting]: types/cast.md
[traits]: trait.md
[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html

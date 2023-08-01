# Moldagem

A Rust não fornece nenhuma conversão (coerção) de tipo implícita entre tipos primitivos. Mas, a conversão (moldagem) de tipo explícita pode ser realizada usando a palavra-chave `as`.

As regras para converter entre tipos integrais segue geralmente as convenções da C, exceto em casos onde a C tem comportamento não definido. O comportamento de todos os moldes entre tipos integrais é bem definido na Rust.

```rust,editable,ignore,mdbook-runnable
// Suprimir todos os avisos dos moldes que transbordam.
#![allow(overflowing_literals)]

fn main() {
    let decimal = 65.4321_f32;

    // Error! Sem conversão implícita
    let integer: u8 = decimal;
    // FIXME ^ Comente esta linha

    // Conversão explícita
    let integer = decimal as u8;
    let character = integer as char;

    // Error! Existem limitações nas regras de conversão.
    // Um flutuante não pode ser diretamente convertido à um carácter.
    let character = decimal as char;
    // FIXME ^ Comente esta linha

    println!("Casting: {} -> {} -> {}", decimal, integer, character);

    // quando moldamos qualquer valor à um tipo sem sinal, T,
    // T::MAX + 1 é adicionado ou subtraído até o valor caber num novo tipo

    // 1000 já cabe num u16
    println!("1000 as a u16 is: {}", 1000 as u16);

    // 1000 - 256 - 256 - 256 = 232
    // Nos bastidores, o primeiro os bits menos significativos de 8 são mantidos,
    // enquanto o resto perto do bit mais significativo é truncado.
    println!("1000 as a u8 is : {}", 1000 as u8);
    // -1 + 256 = 255
    println!("  -1 as a u8 is : {}", (-1i8) as u8);

    // Para os números positivos, isto é o mesmo que modulus
    println!("1000 mod 256 is : {}", 1000 % 256);

    // Quando moldamos à um tipo com sinal, o resultado (bitwise) é o mesmo que
    // a primeira moldagem ao tipo sem sinal correspondente.
    // Se o bit mais significativo deste valor for 1, então o valor é negativo.

    // A menos que já caiba, claro.
    println!(" 128 as a i16 is: {}", 128 as i16);

    // 128 as u8 -> 128,
    // cujo valor na representação de complemento dos dois de 8-bit é:
    println!(" 128 as a i8 is : {}", 128 as i8);

    // repetindo o exemplo acima
    // 1000 as u8 -> 232
    println!("1000 as a u8 is : {}", 1000 as u8);
    // e o valor de 232 na representação de complemento dos dois de 8-bit é -24
    println!(" 232 as a i8 is : {}", 232 as i8);

    // Desde a Rust 1.45, a palavra-chave `as` realiza um *molde de saturação*
    // quando moldamos de flutuante à inteiro. Se o valor de ponto flutuante
    // excede o saldo máximo ou é menos do que o saldo mínimo, o valor
    // retornado será igual ao salto cruzado.

    // 300.0 as u8 é 255
    println!(" 300.0 as u8 is : {}", 300.0_f32 as u8);
    // -100.0 as u8 é 0
    println!("-100.0 as u8 is : {}", -100.0_f32 as u8);
    // nan as u8 é 0
    println!("   nan as u8 is : {}", f32::NAN as u8);

    // Este comportamento incorre num pequeno custo de execução e
    // pode ser evitado com métodos inseguros, no entanto o resultado pode
    // transbordar e retornar **valores incertos**. Use estes métodos sabiamente:
    unsafe {
        // 300.0 as u8 é 44
        println!(" 300.0 as u8 is : {}", 300.0_f32.to_int_unchecked::<u8>());
        // -100.0 as u8 é 156
        println!("-100.0 as u8 is : {}", (-100.0_f32).to_int_unchecked::<u8>());
        // nan as u8 é 0
        println!("   nan as u8 is : {}", f32::NAN.to_int_unchecked::<u8>());
    }
}
```

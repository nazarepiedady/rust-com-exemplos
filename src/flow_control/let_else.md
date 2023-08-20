# `let-else`

> 🛈 estável desde a: rust 1.65

Com `let`-`else`, um padrão refutável pode corresponder e vincular variáveis no âmbito envolvente como um `let` normal, se não diverge (por exemplo, `break`, `return`, `panic!`) quando o padrão não corresponder:

```rust
use std::str::FromStr;

fn get_count_item(s: &str) -> (u64, &str) {
    let mut it = s.split(' ');
    let (Some(count_str), Some(item)) = (it.next(), it.next()) else {
        panic!("Can't segment count item pair: '{s}'");
    };
    let Ok(count) = u64::from_str(count_str) else {
        panic!("Can't parse integer: '{count_str}'");
    };
    (count, item)
}

assert_eq!(get_count_item("3 chairs"), (3, "chairs"));
```

O âmbito de vínculos de nome é a coisa principal que torna isto diferente de `match` ou expressões `if let`-`else`. Nós poderíamos anteriormente aproximar estes padrões com um lamentável bit de repetição e um `let` externo:

```rust
# use std::str::FromStr;
# 
# fn get_count_item(s: &str) -> (u64, &str) {
#     let mut it = s.split(' ');
    let (count_str, item) = match (it.next(), it.next()) {
        (Some(count_str), Some(item)) => (count_str, item),
        _ => panic!("Can't segment count item pair: '{s}'"),
    };
    let count = if let Ok(count) = u64::from_str(count_str) {
        count
    } else {
        panic!("Can't parse integer: '{count_str}'");
    };
#     (count, item)
# }
# 
# assert_eq!(get_count_item("3 chairs"), (3, "chairs"));
```

### Consulte também:

[`option`][option], [`match`][match], [`if let`][if_let] e o [RFC de `let-else`][let_else_rfc].


[match]: ./match.md
[if_let]: ./if_let.md
[let_else_rfc]: https://rust-lang.github.io/rfcs/3137-let-else.html
[option]: ../std/option.md
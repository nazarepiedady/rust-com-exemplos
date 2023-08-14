# Encaixamentos e Rótulos

É possível rebentar (`break`) ou ignorar (`continue`) laços de repetição externos quando lidamos com laços de repetição encaixados. Nestes casos, os laços devem ser anotados com o mesmo rótulo (`'label`), e o rótulo deve ser passado à declaração `break` ou `continue`.

```rust,editable
#![allow(unreachable_code, unused_labels)]

fn main() {
    'outer: loop {
        println!("Entered the outer loop");

        'inner: loop {
            println!("Entered the inner loop");

            // Isto apenas rebentaria o laço de repetição interno
            //break;

            // Isto rebenta o laço de repetição externo
            break 'outer;
        }

        println!("This point will never be reached");
    }

    println!("Exited the outer loop");
}
```

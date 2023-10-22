# Funções e Métodos Associados

Algumas funções são conectadas à um topo específico. Existem em duas formas: funções associadas, e métodos. As funções associadas são funções que são definidas geralmente sobre um tipo, enquanto os métodos são funções associadas que são chamados sobre uma instância específica dum tipo:

```rust,editable
struct Point {
    x: f64,
    y: f64,
}

// Bloco de implementação, todas funções associadas do `Point`
// e os métodos são colocados neste bloco
impl Point {
    // Isto é uma "função associada" pois esta função está associada à
    // um tipo específico, que é, `Point`.
    //
    // Funções associadas não precisam ser chamadas com uma instância.
    // Estas funções são geralmente usadas como construtoras.
    fn origin() -> Point {
        Point { x: 0.0, y: 0.0 }
    }

    // Uma outra função associada, recebendo dois argumentos:
    fn new(x: f64, y: f64) -> Point {
        Point { x: x, y: y }
    }
}

struct Rectangle {
    p1: Point,
    p2: Point,
}

impl Rectangle {
    // Isto é um método
    // `&self` é açúcar sintático para `self: &Self`,
    // aonde `Self` é o tipo do objeto chamador.
    // Neste caso `Self` = `Rectangle`
    fn area(&self) -> f64 {
        // `self` dá acesso aos campos da estrutura através do
        // operador ponto
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        // `abs` é um método de `f64` que retorna o
        // valor absoluto do chamador
        ((x1 - x2) * (y1 - y2)).abs()
    }

    fn perimeter(&self) -> f64 {
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        2.0 * ((x1 - x2).abs() + (y1 - y2).abs())
    }

    // Este método exige que objeto chamador seja mutável.
    // `&mut self` é açúcar para `self: &mut Self`
    fn translate(&mut self, x: f64, y: f64) {
        self.p1.x += x;
        self.p2.x += x;

        self.p1.y += y;
        self.p2.y += y;
    }
}

// `Pair` possui os recursos: dois amontoados alocados de inteiros
struct Pair(Box<i32>, Box<i32>);

impl Pair {
    // Este método "consome" os recursos do objeto chamador
    // `self` é açúcar para `self: Self`
    fn destroy(self) {
        // Desestruturar `self`
        let Pair(first, second) = self;

        println!("Destroying Pair({}, {})", first, second);

        // `first` e `second` saem do âmbito e são liberados
    }
}

fn main() {
    let rectangle = Rectangle {
        // As funções associadas são chamadas usando dois-pontos duplos
        p1: Point::origin(),
        p2: Point::new(3.0, 4.0),
    };

    // Os métodos são chamados usando o operador ponto
    // Nota que o primeiro argumento `&self` é implicitamente passado, isto é,
    // `rectangle.perimeter()` === `Rectangle::perimeter(&rectangle)`
    println!("Rectangle perimeter: {}", rectangle.perimeter());
    println!("Rectangle area: {}", rectangle.area());

    let mut square = Rectangle {
        p1: Point::origin(),
        p2: Point::new(1.0, 1.0),
    };

    // Error! `rectangle` é imutável, mas este método exige um objeto mutável
    //rectangle.translate(1.0, 0.0);
    // TODO ^ Tente desfazer o comentário desta linha

    // Okay! Os objetos mutáveis podem chamar métodos mutáveis
    square.translate(1.0, 1.0);

    let pair = Pair(Box::new(1), Box::new(2));

    pair.destroy();

    // Error! A chama de `destroy` anterior "consumiu" `pair`
    //pair.destroy();
    // TODO ^ Tente desfazer o comentário desta linha
}
```

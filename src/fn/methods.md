# Funções associadas e Métodos

Algumas funções são conectadas a um tipo específico. Existem dois tipos: funções associadas, e métodos. Funções associadas são funções que são definidas de modo geral para um tipo, já métodos são funções associadas chamadas para uma instância particular de um tipo.

```rust,editable
struct Point {
    x: f64,
    y: f64,
}

// Bloco de implementação, todas funções associadas e métodos de `Point` vão aqui
impl Point {
    // Isto é uma "função associada" pois essa função está associada com
    // um tipo particular, neste caso, `Point`.
    //
    // Funções associadas não precisam ser chamadas com uma instância.
    // Estas funções são comumente usadas como construtores.
    fn origin() -> Point {
        Point { x: 0.0, y: 0.0 }
    }

    // Outra função associada, tomando dois argumentos:
    fn new(x: f64, y: f64) -> Point {
        Point { x: x, y: y }
    }
}

struct Rectangle {
    p1: Point,
    p2: Point,
}

impl Retangulo {
    // Isto é um método
    // `&self` é açúcar sintático para `self: &Self`, aonde `Self` é o tipo do objeto
    // `self`. Neste caso `Self` = `Retangulo`
    fn area(&self) -> f64 {
        // `self` dá acesso aos campos da struct através do operador de ponto (`self.`)
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        // `abs` é um método de `f64` que retorna o valor absoluto do `f64`
        ((x1 - x2) * (y1 - y2)).abs()
    }

    fn perimeter(&self) -> f64 {
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        2.0 * ((x1 - x2).abs() + (y1 - y2).abs())
    }

    // Este método requer que o objeto chamado seja mutável.
    // `&mut self` é açúcar para `self: &mut Self`
    fn translate(&mut self, x: f64, y: f64) {
        self.p1.x += x;
        self.p2.x += x;

        self.p1.y += y;
        self.p2.y += y;
    }
}

// `Pair` possui recursos: dois inteiros alocados na heap
struct Pair(Box<i32>, Box<i32>);

impl Pair {
    // Este método "consome" os recursos do objeto chamado
    // `self` é açúcar para `self: Self`
    fn destroy(self) {
        // Desestruturando `self`
        let Pair(first, second) = self;

        println!("Destroying Pair({}, {})", first, second);

        // `first` e `second` saem do escopo e são liberados
    }
}

fn main() {
    let rectangle = Rectangle {
        // Funções associadas são chamadas usando dois dois-pontos
        p1: Point::origin(),
        p2: Point::new(3.0, 4.0),
    };

    // Métodos são chamados usando o operador ponto
    // Note que o primeiro argumento `&self` é implicitamente passado, isto é,
    // `rectangle.perimeter()` === `Rectangle::perimeter(&rectangle)`
    println!("Rectangle perimeter: {}", rectangle.perimeter());
    println!("Rectangle area: {}", rectangle.area());

    let mut square = Rectangle {
        p1: Point::origin(),
        p2: Point::new(1.0, 1.0),
    };

    // Erro! `rectangle` é imutável, mas esse método requer um objeto mutável
    //rectangle.translate(1.0, 0.0);
    // TODO ^ Tente descomentar essa linha

    // Ok! Objetos mutáveis podem chamar métodos mutáveis
    square.translate(1.0, 1.0);

    let pair = Pair(Box::new(1), Box::new(2));

    pair.destroy();

    // Erro! Anterior chamada à `destroy` "consumiu" variável `pair`
    //pair.destroy();
    // TODO ^ Tente descomentar essa linha
}
```

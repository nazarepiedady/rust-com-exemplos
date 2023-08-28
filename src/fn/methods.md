# Funções associadas e Métodos

Algumas funções são conectadas a um tipo específico. Existem dois tipos: funções associadas, e métodos. Funções associadas são funções que são definidas de modo geral para um tipo, já métodos são funções associadas chamadas para uma instância particular de um tipo.

```rust,editable
struct Ponto {
    x: f64,
    y: f64,
}

// Bloco de implementação, todas funções associadas e métodos de `Ponto` vão aqui
impl Ponto {
    // Isto é uma "função associada" pois essa função está associada com
    // um tipo particular, neste caso, `Ponto`.
    //
    // Funções associadas não precisam ser chamadas com uma instância.
    // Estas funções são comumente usadas como construtores.
    fn origem() -> Ponto {
        Ponto { x: 0.0, y: 0.0 }
    }

    // Outra função associada, tomando dois argumentos:
    fn new(x: f64, y: f64) -> Ponto {
        Ponto { x: x, y: y }
    }
}

struct Retangulo {
    p1: Ponto,
    p2: Ponto,
}

impl Retangulo {
    // Isto é um método
    // `&self` é açúcar sintático para `self: &Self`, aonde `Self` é o tipo do objeto
    // `self`. Neste caso `Self` = `Retangulo`
    fn area(&self) -> f64 {
        // `self` dá acesso aos campos da struct através do operador de ponto (`self.`)
        let Ponto { x: x1, y: y1 } = self.p1;
        let Ponto { x: x2, y: y2 } = self.p2;

        // `abs` é um método de `f64` que retorna o valor absoluto do `f64`
        ((x1 - x2) * (y1 - y2)).abs()
    }

    fn perimetro(&self) -> f64 {
        let Ponto { x: x1, y: y1 } = self.p1;
        let Ponto { x: x2, y: y2 } = self.p2;

        2.0 * ((x1 - x2).abs() + (y1 - y2).abs())
    }

    // Este método requer que o objeto chamado seja mutável.
    // `&mut self` é açúcar para `self: &mut Self`
    fn traduzir(&mut self, x: f64, y: f64) {
        self.p1.x += x;
        self.p2.x += x;

        self.p1.y += y;
        self.p2.y += y;
    }
}

// `Par` possui recursos: dois inteiros alocados na heap
struct Par(Box<i32>, Box<i32>);

impl Par {
    // Este método "consome" os recursos do objeto chamado
    // `self` é açúcar para `self: Self`
    fn destruir(self) {
        // Desestruturando `self`
        let Par(primeiro, segundo) = self;

        println!("Destruindo Par({}, {})", primeiro, segundo);

        // `primeiro` e `segundo` saem do escopo e são liberados
    }
}

fn main() {
    let retangulo = Retangulo {
        // Funções associadas são chamadas usando dois dois-pontos
        p1: Ponto::origem(),
        p2: Ponto::new(3.0, 4.0),
    };

    // Métodos são chamados usando o operador ponto
    // Note que o primeiro argumento `&self` é implicitamente passado, isto é,
    // `retangulo.perimetro()` === `Retangulo::perimetro(&retangulo)`
    println!("Retangulo perimetro: {}", retangulo.perimetro());
    println!("Retangulo area: {}", retangulo.area());

    let mut quadrado = Retangulo {
        p1: Ponto::origem(),
        p2: Ponto::new(1.0, 1.0),
    };

    // Erro! `retangulo` é imutável, mas esse método requer um objeto mutável
    //retangulo.traduzir(1.0, 0.0);
    // LEMBRETE ^ Tente descomentar essa linha

    // Ok! Objetos mutáveis podem chamar métodos mutáveis
    quadrado.traduzir(1.0, 1.0);

    let par = Par(Box::new(1), Box::new(2));

    par.destruir();

    // Erro! Anterior chamada à `destruir` "consumiu" variável `par`
    //par.destruir();
    // LEMBRETE ^ Tente descomentar essa linha
}
```

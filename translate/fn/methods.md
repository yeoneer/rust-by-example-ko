# 메소드

메소드는 객체에 소속된 함수입니다.
메소드는 `impl` 블랙 내에 정의되며,
`self` 키워드로 객체의 데이터 및 타 메소드에 접근 가능합니다.

```rust,editable
struct Point {
    x: f64,
    y: f64,
}

// 구현 블록입니다. 모든 `Point` 메소드는 이곳에 정의됩니다.
impl Point {
    // 다음은 static 메소드입니다.
    // static 메소드는 인스턴스 없이 호출 가능합니다.
    // 일반적으로, 생성자로 이용됩니다.
    fn origin() -> Point {
        Point { x: 0.0, y: 0.0 }
    }

    // 두 인수를 갖는 또 다른 static 메소드입니다.
    fn new(x: f64, y: f64) -> Point {
        Point { x: x, y: y }
    }
}

struct Rectangle {
    p1: Point,
    p2: Point,
}

impl Rectangle {
    // 다음은 인스턴스 메소드입니다.
    // `&self`는 `self: &Self`의 syntac sugar입니다.
    // 이때 `Self`는 호출한 객체의 타입입니다(이 경우 `Self` = `Rectangle`).
    fn area(&self) -> f64 {
        // `self`는 점(`.`) 연산자로 구조체 필드에 접근할 수 있습니다.
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        // `abs`는 호출자(caller)의 절대값을 반환하는
        // `f64` 메소드입니다.
        ((x1 - x2) * (y1 - y2)).abs()
    }

    fn perimeter(&self) -> f64 {
        let Point { x: x1, y: y1 } = self.p1;
        let Point { x: x2, y: y2 } = self.p2;

        2.0 * ((x1 - x2).abs() + (y1 - y2).abs())
    }

    // 다음 메소드는 호출자 객체가 mutable이어야 합니다.
    // `&mut self`는 `self: &mut Self`의 syntac sugar입니다.
    fn translate(&mut self, x: f64, y: f64) {
        self.p1.x += x;
        self.p2.x += x;

        self.p1.y += y;
        self.p2.y += y;
    }
}

// `Pair`는 두 개의 힙 할당된 정수 리소스의 소유권을 소유합니다.
struct Pair(Box<i32>, Box<i32>);

impl Pair {
    // 다음 메소드는 호출자 객체의 리소스를 '소비(consume)'합니다.
    // `self` = `self: Self`
    fn destroy(self) {
        // `self` 해체
        let Pair(first, second) = self;

        println!("Pair를 와해시킵니다({}, {})", first, second);

        // `first`, `second`는 스코프를 벗어나면서 할당 해제됩니다.
    }
}

fn main() {
    let rectangle = Rectangle {
        // static 메소드는 콜론 두 개(`::`)로 호출합니다.
        p1: Point::origin(),
        p2: Point::new(3.0, 4.0),
    };

    // 인스턴스 메소드는 점 연산자(`.`)로 호출합니다.
    // 첫 번째 인수인 `&self`가 암묵적으로 전달되는 것을 유의해주세요.
    // 즉, `rectangle.perimeter()`는 `Rectangle::perimeter(&rectangle)`와 같습니다.
    println!("사각형 둘레: {}", rectangle.perimeter());
    println!("사각형 면적: {}", rectangle.area());

    let mut square = Rectangle {
        p1: Point::origin(),
        p2: Point::new(1.0, 1.0),
    };

    // 에러! `rectangle`는 불변이나,
    // 이 메소드는 가변 객체를 필요로합니다.
    //rectangle.translate(1.0, 0.0);
    // TODO ^ 이 줄을 주석 해제해보세요.

    // 문제없음! 가변 객체로는 호출할 수 있습니다.
    square.translate(1.0, 1.0);

    let pair = Pair(Box::new(1), Box::new(2));

    pair.destroy();

    // 에러! 앞서 호출한 `destroy` 메소드가 `pair`를 소비했습니다.
    //pair.destroy();
    // TODO ^ 이 줄을 주석 해제해보세요.
}
```

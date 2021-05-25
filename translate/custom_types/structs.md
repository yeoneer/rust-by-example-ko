# 구조체

`struct` 키워드로 만들 수 있는 구조체는 세 종류가 있습니다.

* 튜플 구조체 - 간단하게, '이름이 있는 튜플'입니다.
* 전통 [C언어 구조체][c_struct]
* 유닛 구조체 - 필드가 없는 구조체입니다. 제네릭에 사용됩니다.

```rust,editable
#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

// 유닛 구조체
struct Unit;

// 튜플 구조체
struct Pair(i32, f32);

// 두 개의 필드를 가진 구조체
struct Point {
    x: f32,
    y: f32,
}

// 구조체는 또 다른 구조체의 필드가 될 수 있습니다.
#[allow(dead_code)]
struct Rectangle {
    // 사각형은 좌측 상단 꼭짓점과 우측 하단 꼭짓점이 공간의 어디에
    // 위치해 있는지로 나타낼 수 있습니다.
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // 필드 초기화 축약법으로 구조체를 생성합니다.
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };

    // debug 출력으로 구조체를 출력합니다.
    println!("{:?}", peter);


    // `Point` 구조체 인스턴스를 생성합니다.
    let point: Point = Point { x: 10.3, y: 0.4 };

    // point 인스턴스의 필드에 접근합니다.
    println!("point 좌표: ({}, {})", point.x, point.y);

    // 구조체 갱신 문법을 사용해 기존 구조체 인스턴스의 필드로 새로운 구조체
    // 인스턴스를 생성합니다.
    let bottom_right = Point { x: 5.2, ..point };

    // `point`의 필드로 `bottom_right`를 생성했으므로,
    // `bottom_right.y`는 `point.y`와 같습니다.
    println!("두 번째 point 좌표: ({}, {})", bottom_right.x, bottom_right.y);

    // `let` 구문으로 point를 해체하여 바인딩합니다.
    let Point { x: top_edge, y: left_edge } = point;

    let _rectangle = Rectangle {
        // 구조체 인스턴스 생성문도 표현식입니다.
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };

    // 유닛 구조체 생성문입니다.
    let _unit = Unit;

    // 튜플 구조체를 생성합니다.
    let pair = Pair(1, 0.1);

    // 튜플 구조체 필드에 접근합니다
    println!("pair에는 {:?}, {:?}이 들어있습니다", pair.0, pair.1);

    // 튜플 구조체를 해체합니다
    let Pair(integer, decimal) = pair;

    println!("pair에는 {:?}, {:?}이 들어있습니다", integer, decimal);
}
```

### 실습

1. 사각형의 면적을 계산하는 `react_area` 함수를 추가해보세요.
   (중첩 해체 구문을 사용해보세요.)
2. `Point`, `f32`를 매개변수로 전달받는 `square` 함수를 추가해보세요.
   `Point`를 좌측 하단 꼭짓점으로 사용하고, `f32` 값을 너비, 높이로
   사용하는 `Rectangle`을 반환해야합니다.

### See also

[`attributes`][attributes], [destructuring][destructuring]

[attributes]: ../attribute.md
[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[destructuring]: ../flow_control/match/destructuring.md

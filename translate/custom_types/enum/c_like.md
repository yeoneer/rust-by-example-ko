# C-like

열거형은 C언어에서처럼 사용할 수도 있습니다.

```rust,editable
// 사용하지 않은 코드(unused code) 경고를 숨기기 위한 속성입니다.
#![allow(dead_code)]

// 암묵적 식별자(0부터 시작)를 사용한 열거형
enum Number {
    Zero,
    One,
    Two,
}

// 명시적 식별자를 사용한 열거형
enum Color {
    Red = 0xff0000,
    Green = 0x00ff00,
    Blue = 0x0000ff,
}

fn main() {
    // 열거형은 정수로 형 변환할 수 있습니다.
    println!("Zero는 {}입니다", Number::Zero as i32);
    println!("One은 {}입니다", Number::One as i32);

    println!("장미 색은 #{:06x}입니다", Color::Red as i32);
    println!("제비꽃 색은 #{:06x}입니다", Color::Blue as i32);
}
```

### See also:

[casting][cast]

[cast]: ../../types/cast.md

# `From`, `Into`

[`From`], [`Into`] 트레잇은 본질적으로 서로 이어져있으며,
실제 구현 또한 마찬가지입니다. A 타입을 B 타입으로 변환할 수 있다면,
B 타입을 A 타입으로 변환할 수도 있어야 하는 건 당연한 일이죠.

## `From`

[`From`] 트레잇으로는 어떠한 타입을 다른 타입으로부터 어떻게 생성하는지 정의할 수 있습니다.
이를 이용하면 여러 타입 간에 쉽게 변환할 수 있습니다.
기본 타입 및 공용 타입은 표준 라이브러리에 수많은 `From` 트레잇 구현이
이미 작성되어있습니다.

그 예로, `str`은 `String`으로 쉽게 변환할 수 있죠.

```rust
let my_str = "hello";
let my_string = String::from(my_str);
```

우리가 직접 만든 타입도 변환 방법을 정의해주면 쉽게 변환 가능합니다.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let num = Number::from(30);
    println!("내가 만든 Number {:?}", num);
}
```

## `Into`

[`Into`] 트레잇은 단순히 `From` 트레잇의 반대입니다.
즉, `From` 트레잇이 구현된 여러분의 타입에 `Into`를 사용하면
`from`이 호출됩니다.

`Into` 트레잇을 사용하는 대부분의 경우,
컴파일러는 알맞은 타입을 알아낼 수 없으므로 타입 명시가 필수적입니다.
하지만 이건 얻는 이점에 비하면 사소한 문제입니다.

```rust,editable
use std::convert::From;

#[derive(Debug)]
struct Number {
    value: i32,
}

impl From<i32> for Number {
    fn from(item: i32) -> Self {
        Number { value: item }
    }
}

fn main() {
    let int = 5;
    // 타입 선언을 지워보세요
    let num: Number = int.into();
    println!("Number는 {:?}입니다", num);
}
```

[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html

# 문자열 변환

## 문자열로 변환하기

어떤 타입에 [`ToString`] 트레잇이 구현되어있다면 `String`으로 변환할 수 있습니다.
다만, 타입에 [`ToString`]을 직접 구현하는 대신, [`fmt::Display`][Display] 트레잇을 구현해
[`ToString`]을 자동으로 생성하고 [`print!`][print]에서 다룬 타입 출력도
가능하게 만들 수 있습니다.

```rust,editable
use std::fmt;

struct Circle {
    radius: i32
}

impl fmt::Display for Circle {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "반지름이 {}인 원", self.radius)
    }
}

fn main() {
    let circle = Circle { radius: 6 };
    println!("{}", circle.to_string());
}
```

## 문자열 파싱하기

문자열을 다른 타입으로 변환하는 문자열 파싱은
일반적으로 [`parse`] 함수가 사용되며, 여기에 타입 추론을 붙이거나
'turbofish' 구문으로 타입을 명시합니다.
다음 예제는 각각의 방법으로 문자열을 숫자로 변환하는 예시를 나타냅니다.

어떤 타입에 [`FromStr`] 트레잇이 구현되어있다면, 문자열을 해당 타입으로 변환할 수 있습니다.
표준 라이브러리 내에는 다양한 타입에 대해서 [`FromStr`] 트레잇이 구현되어있습니다.
사용자 정의 타입에도 [`FromStr`] 트레잇을 구현하면
마찬가지 동작이 가능합니다.

```rust,editable
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed = "10".parse::<i32>().unwrap();

    let sum = parsed + turbo_parsed;
    println!("합계: {:?}", sum);
}
```

[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[Display]: https://doc.rust-lang.org/std/fmt/trait.Display.html
[print]: ../hello/print.md
[`parse`]: https://doc.rust-lang.org/std/primitive.str.html#method.parse
[`FromStr`]: https://doc.rust-lang.org/std/str/trait.FromStr.html

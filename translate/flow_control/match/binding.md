# 바인딩

변수에 간접적으로 접근하면 분기 이후에 다시 바인딩하지 않고는
해당 변수를 사용할 수 없습니다. `match` 에서 `@`를 이용하면
값을 어떤 이름에 바인딩할 수 있습니다.

```rust,editable
// `age` 함수는 `u32` 타입을 반환합니다.
fn age() -> u32 {
    15
}

fn main() {
    println!("당신은 나이는?");

    match age() {
        0             => println!("아직 돌잔치도 못했습니다"),
        // 1 ..= 12에 바로 매칭시킬 수도 있지만,
        // 이 경우 나이 값이 어떤지 알 수 없습니다.
        // `n`에 1 ..= 12를 바인딩하면 나이를 알 수 있습니다.
        n @ 1  ..= 12 => println!("{:?}살 어린이입니다", n),
        n @ 13 ..= 19 => println!("{:?}살 청소년입니다", n),
        // 바인딩 된 것이 없습니다. 결과를 반환합니다.
        n             => println!("{:?}세 성인입니다.", n),
    }
}
```

바인딩으로 `enum` variant를 해체할 수도 있습니다. `Option`처럼 말이죠.

```rust,editable
fn some_number() -> Option<u32> {
    Some(42)
}

fn main() {
    match some_number() {
        // `Some` variant를 얻어내고, 값이 42로 일치하면
        // `n`에 바인딩합니다.
        Some(n @ 42) => println!("답: {}!", n),
        // 그 외 값에 매칭
        Some(n)      => println!("관심 없음... {}", n),
        // 어떤 것과도 매칭되지 않음 (`None` variant일 경우).
        _            => (),
    }
}
```

### See also:

[함수][functions], [열거형][enums], [`Option`][option]

[functions]: ../../fn.md
[enums]: ../../custom_types/enum.md
[option]: ../../std/option.md

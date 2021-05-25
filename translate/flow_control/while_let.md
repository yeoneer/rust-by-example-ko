# while let

`if let` 처럼, `while let`을 사용하면 불편한 `macth` 배열을
더 괜찮게 바꿀 수 있습니다. `i`를 증가시키는 예시를 생각해보죠.

```rust
// `Option<i32>` 타입 `optional`를 생성합니다
let mut optional = Some(0);

// 반복해서 검사합니다.
loop {
    match optional {
        // `optional`이 해체되었다면 블록을 평가합니다.
        Some(i) => {
            if i > 9 {
                println!("9보다 큽니다. 끝!");
                optional = None;
            } else {
                println!("`i`는 `{:?}입니다`. 다시 시도합니다.", i);
                optional = Some(i + 1);
            }
            // ^ 들여쓰기를 세 번이나 해야 합니다!
        },
        // 해체 실패 시 반복문을 이탈합니다.
        _ => { break; }
        // ^ 굳이 필요할까요? 더 좋은 방법을 찾아봅시다!
    }
}
```

`while let`을 사용하면 훨씬 나아집니다.

```rust,editable
fn main() {
    // `Option<i32>` 타입 `optional`를 생성합니다
    let mut optional = Some(0);

    // 여긴 다음과 같이 읽습니다. "`optional`이 `Some(i)`로
    // 해체 가능한 동안에는 블록(`{}`)을 평가하고, 아니라면 `break` 해라."
    while let Some(i) = optional {
        if i > 9 {
            println!("9보다 큽니다. 끝!");
            optional = None;
        } else {
            println!("`i`는 `{:?}입니다`. 다시 시도합니다.", i);
            optional = Some(i + 1);
        }
        // ^ 오른쪽으로 덜 밀려났으며, 해체 실패한 경우를
        // 명시적으로 처리할 필요가 없습니다.
    }
    // ^ `if let`에는 `else`/`else if`를 추가할 수 있지만,
    // `while let`은 불가능합니다.
}
```

### See also:

[열거형][enum], [`Option`][option], [RFC][while_let_rfc]

[enum]: ../custom_types/enum.md
[option]: ../std/option.md
[while_let_rfc]: https://github.com/rust-lang/rfcs/pull/214

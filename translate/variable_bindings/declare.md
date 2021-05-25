# 조기 선언

변수 바인딩을 먼저 선언하고, 나중에 초기화할 수도 있습니다.
다만, 이러한 형식은 초기화되지 않은 변수 사용을 유발할 수 있으므로 자주 사용되지는
않습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 변수 바인딩 선언
    let a_binding;

    {
        let x = 2;

        // 바인딩 초기화
        a_binding = x * x;
    }

    println!("a_binding: {}", a_binding);

    let another_binding;

    // 에러! 초기화되지 않은 바인딩 사용
    println!("another binding: {}", another_binding);
    // 고쳐주세요! ^ 이 줄을 주석 처리해주세요

    another_binding = 1;

    println!("another_binding: {}", another_binding);
}
```

초기화되지 않은 변수 사용은 정의되지 않은 행동(Undefined behavior)을 유발할 수 있으므로,
컴파일러가 금지합니다.

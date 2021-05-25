# 가변성

변수 바인딩은 기본적으로 불변(immutable)이지만,
`mut` 수식어를 사용하면 가변성(mutability)을 갖도록 바꿀 수 있습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let _immutable_binding = 1;
    let mut mutable_binding = 1;

    println!("변하기 전: {}", mutable_binding);

    // 문제없음
    mutable_binding += 1;

    println!("변한 후: {}", mutable_binding);

    // 에러!
    _immutable_binding += 1;
    // 고쳐주세요! ^ 이 줄을 주석 처리해주세요
}
```

컴파일러가 가변성 에러 진단 메시지를 상세히 표시할 겁니다.

# 스코프, 변수 가리기

변수 바인딩은 스코프(scope, 범위)를 가지며, **블록** 내에서만 존재할 수 있습니다.
블록은 `{}` 로 둘러싸인 구문의 모음을 의미합니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 메인 함수 내에서 존재하는 바인딩
    let long_lived_binding = 1;

    // 메인 함수보다는 스코프가 작은 블록입니다.
    {
        // 이 블록 내에서만 존재하는 바인딩
        let short_lived_binding = 2;

        println!("내부에서의 수명 짧은 바인딩: {}", short_lived_binding);
    }
    // 블록 끝

    // 에러! `short_lived_binding`는 이 스코프에 존재하지 않습니다.
    println!("외부에서의 수명 짧은 바인딩: {}", short_lived_binding);
    // 고쳐주세요! ^ 이 줄을 주석 처리해주세요.

    println!("외부에서의 수명 긴 바인딩: {}", long_lived_binding);
}
```

또한, 변수는 가려질 수 있습니다. ([variable shadowing][variable-shadow])

```rust,editable,ignore,mdbook-runnable
fn main() {
    let shadowed_binding = 1;

    {
        println!("가려지기 전: {}", shadowed_binding);

        // 외부의 바인딩을 *가리는* 바인딩
        let shadowed_binding = "abc";

        println!("내부 블록에서 가려진 후: {}", shadowed_binding);
    }
    println!("내부 블록 벗어남: {}", shadowed_binding);

    // 기존 바인딩을 *가리는* 바인딩
    let shadowed_binding = 2;
    println!("외부 블록에서 가려진 후: {}", shadowed_binding);
}
```

[variable-shadow]: https://en.wikipedia.org/wiki/Variable_shadowing

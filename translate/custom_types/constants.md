# 상수

러스트에는 두 종류 상수가 있습니다. 전역 범위를 포함한 모든 스코프에 선언 가능하며,
타입을 반드시 명시해야 합니다.

* `const`: 변경 불가능한 값 (보편적인 상수입니다).
* `static`: `mut` 키워드를 이용하면 변경 가능한 변수입니다.
  [`'static`][static] 라이프타임을 갖습니다.
  static 라이프타임은 자동으로 추론되며, 명시할 필요 없습니다.
  변경 가능한 static 변수에의 접근 및 수정은 `unsafe` 연산입니다.

```rust,editable,ignore,mdbook-runnable
// 모든 스코프를 벗어난 전역 범위에 선언합니다.
static LANGUAGE: &str = "Rust";
const THRESHOLD: i32 = 10;

fn is_big(n: i32) -> bool {
    // 함수 내에서 상수에 접근합니다.
    n > THRESHOLD
}

fn main() {
    let n = 16;

    // 메인 스레드 내에서 상수에 접근합니다.
    println!("프로그래밍 언어 {}", LANGUAGE);
    println!("임계치는 {}입니다", THRESHOLD);
    println!("{}은 {} 값입니다", n, if is_big(n) { "큰" } else { "작은" });

    // 에러! `const`는 수정할 수 없습니다.
    THRESHOLD = 5;
    // 고쳐주세요! ^ 이 줄을 주석 처리해주세요.
}
```

### See also:

[The `const`/`static` RFC](
https://github.com/rust-lang/rfcs/blob/master/text/0246-const-vs-static.md),
[`'static` lifetime][static]

[static]: ../scope/lifetime/static_lifetime.md
[unsafe]: ../unsafe.md

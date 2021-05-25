# 출력 포맷팅

출력은 [`std::fmt`][fmt]에 정의된 [`매크로`][macros]를 이용합니다.

* `format!`: 작성한 포맷팅대로 [`String`][string]을 생성합니다.
* `print!`: `format!`과 동일하지만, 문자열을 콘솔(io::stdout)로 출력합니다.
* `println!`: `print!`와 동일하지만, 줄바꿈이 추가됩니다.
* `eprint!`: `format!`과 동일하지만, 문자열을 표준 에러(io::stderr)로 출력합니다.
* `eprintln!`: `eprint!`와 동일하지만, 줄바꿈이 추가됩니다.

문자열을 구문 분석하는 방법은 모두 동일합니다.
여담으로, 러스트는 컴파일타임에 포맷팅이 올바르게 작성됐는지 검사합니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // `{}`는 문자열화된 인수로 자동 대체됩니다.
    println!("{}일", 31);

    // 접미사를 따로 붙이지 않으면 31는 i32 타입으로 지정됩니다.
    // 접미사를 붙이면 원하는 타입으로 변경할 수 있습니다. (31i64는 i64타입이 됩니다.)

    // 필요하다면 다양한 패턴을 사용할 수 있습니다.
    // 위치 지정 인수 사용 예시입니다.
    println!("{0} 님, 이분은 {1} 님입니다. {1} 님, 이분은 {0} 님입니다.", "홍길동", "김철수");

    // 명명 인수 사용 예시입니다.
    println!("{subject} {object} {verb}",
             object="헌 쳇바퀴에",
             subject="다람쥐",
             verb="타고파");

    // 특수 포맷팅은 `:`에 붙여서 명시합니다.
    println!("사람들 중 {}/{:b} 은 이진법을 알고 있으며, 나머지 절반은 모릅니다.", 1, 2);

    // 지정한 길이 내 문자열을 우측 정렬합니다.
    // 공백 5칸과 "1" 이 붙은 "     1" 을 출력합니다.
    println!("{number:>width$}", number=1, width=6);

    // 0으로 나머지 숫자를 채웁니다. "000001" 을 출력합니다.
    println!("{number:0>width$}", number=1, width=6);

    // 러스트는 사용된 인수의 개수가 틀리지 않았는지 검사합니다.
    println!("제 이름은 {0}, {1} {0}입니다.", "홍");
    // 고쳐주세요! ^ 인수에 "길동"을 추가해주세요

    // `i32` 값을 갖는 `Structure` 구조체를 생성합니다.
    #[allow(dead_code)]
    struct Structure(i32);

    // 안타깝게도, 구조체같은 사용자 정의 타입은 다루기 좀 까다롭습니다.
    // 다음 코드는 작동하지 않습니다.
    println!("이 구조체는 출력할 수 없어요... `{}`", Structure(3));
    // 고쳐주세요! ^ 이 줄을 주석 처리해주세요
}
```

[`std::fmt`][fmt]에는 문자열 출력을 제어하는 여러 [`트레잇`][traits]이 있습니다.
두 가지 중요한 트레잇의 기본 형태는 다음과 같습니다.

* `fmt::Debug`: `{:?}`로 표시합니다. 문자열을 디버깅하기 좋은 형태로 포맷팅합니다.
* `fmt::Display`: `{}`로 표시합니다. 문자열을 사용자가 보기 좋게 포맷팅합니다.

기본 타입들은 표준 라이브러리에서 `fmt::Display` 트레잇을 구현해두었습니다.
따라서 기본 타입은 별도의 작업 없이 바로 `{}` 로 포맷팅할 수 있지만, 사용자 정의 타입은 추가 작업이 필요합니다

`fmt::Display` 트레잇을 구현하면 [`ToString`] 트레잇이 자동으로 구현되어
해당 타입을 [`String`][string]으로 [변환][convert]할 수 있습니다.

### 실습

 * 앞선 코드의 문제점('고쳐주세요!'로 표시)을 수정하여 오류 없이
   실행되도록 만들어보세요.
 * `Pi는 약 3.142입니다`를 출력하는 `println!` 매크로를 추가해보세요.
   `let pi = 3.141592` 코드로 원주율을 계산하고, 표시할 소수점 자리수를
   조정하세요. (힌트: 표시할 소수점 자리수를 지정하는 방법은
   [`std::fmt`][fmt]에서 찾아볼 수 있습니다)

### See also:

[`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
and [`traits`][traits]

[`std::fmt`][fmt], [`매크로`][macros], [`구조체`][structs],
[`트레잇`][traits]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md

# 타입 별칭

`type` 구문으로 기존 타입에 새로운 이름을 지어줄 수도 있습니다.
타입명은 반드시 대문자 낙타 표기법(`UpperCamelCase`)을 따라야 하며, 따르지 않을 경우 컴파일러 경고가 발생합니다.
단, `usize`, `f32` 등 기본 타입은 이 규칙에서 예외입니다.

```rust,editable
// `NanoSecond`는 `u64`의 새로운 별칭입니다.
type NanoSecond = u64;
type Inch = u64;

// 속성을 사용해 경고를 무시합니다
#[allow(non_camel_case_types)]
type u64_t = u64;
// TODO ^ 속성을 제거해보세요

fn main() {
    // `NanoSecond` = `Inch` = `u64_t` = `u64`.
    let nanoseconds: NanoSecond = 5 as u64_t;
    let inches: Inch = 2 as u64_t;

    // 타입 별칭이 추가적인 타입 안정성을 제공하지는 *않는다는* 점을 알아두세요.
    // 별칭일 뿐 새로운 타입이 *아닙니다*
    println!("{} nanoseconds + {} inches = {} unit?",
             nanoseconds,
             inches,
             nanoseconds + inches);
}
```

타입 별칭은 주로 보일러플레이트를 줄이기 위해 사용됩니다.
예를 들어, `IoResult<T>` 타입은 `Result<T, IoError>` 라는 긴 타입의 별칭입니다.

### See also:

[속성](../attribute.md)

# 기본 요소

러스트는 다양한 기본 요소(primitives)를 제공합니다.
어떤 것들을 제공하는지 살펴보죠.

### 스칼라 타입

* 부호 있는 정수(signed integer): `i8`, `i16`, `i32`, `i64`, `i128` 및 `isize` (포인트 크기)
* 부호 없는 정수(unsigned integer): `u8`, `u16`, `u32`, `u64`, `u128` 및 `usize` (포인터 크기)
* 부동 소수점(floating point): `f32`, `f64`
* `char` - `'a'`, `'α'`, `'∞'` (각각 4바이트) 등의 유니코드 스칼라 값
* `bool` - `true` 혹은 `false`
* 유닛 타입 `()` - 빈 튜플(`()`) 값만을 의미하는 타입

유닛 타입은 튜플이지만, 여러 값을 포함하지는 않기 때문에
복합 타입으로 간주하지 않습니다.

### 복합 타입

* 배열 (`[1, 2, 3]`)
* 튜플 (`(1, true)`)

모든 변수에는 타입을 명시할 수 있습니다.
숫자는 접미사로도 타입을 명시할 수 있고, 아무것도 작성하지 않고 기본 타입을 이용할 수 있죠.
정수는 `i32` 타입, 소수는 `f64` 타입이 기본 타입입니다.
또한, 러스트는 코드 문맥에서 타입을 추론할 수도 있습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    // 변수에는 타입을 명시할 수 있습니다.
    let logical: bool = true;

    let a_float: f64 = 1.0;  // 일반적인 명시
    let an_integer   = 5i32; // 접미사 명시

    // 기본 타입을 사용할 수도 있습니다.
    let default_float   = 3.0; // `f64`
    let default_integer = 7;   // `i32`
    
    // 타입은 코드 문맥에서 추론될 수도 있습니다.
    let mut inferred_type = 12; // 다른 줄로 인해서 i64 타입으로 추론됩니다
    inferred_type = 4294967296i64;
    
    // 가변 변수 값은 변경 가능합니다.
    let mut mutable = 12; // 가변 `i32`
    mutable = 21;
    
    // 에러! 변수의 타입은 변경할 수 없습니다.
    mutable = true;
    
    // 변수는 가려질(shadowing) 수 있습니다.
    let mutable = true;
}
```

### See also:

[the `std` library][std], [`mut`][mut], [`inference`][inference], [`shadowing`][shadowing]

[std]: https://doc.rust-lang.org/std/
[mut]: variable_bindings/mut.md
[inference]: types/inference.md
[shadowing]: variable_bindings/scope.md

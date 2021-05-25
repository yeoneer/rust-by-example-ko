# Debug

출력 구현체가 존재하지 않는 타입에는 `std::fmt` 포맷팅 트레잇을
사용할 수 없습니다. 러스트가 자동으로 구현체를 제공하는 타입은
`std` 라이브러리 내 타입뿐입니다. 그 외에는 전부 어떤 형태로건
**직접** 구현해야 합니다.

이 문제는 `fmt::Debug` 트레잇으로 쉽게 해결할 수 있습니다.
**모든** 타입은 `fmt::Debug` 트레잇을 `derive` 하여 구현체를 자동으로 생성할 수 있습니다.
이는 `fmt::Display` 트레잇에는 해당되지 않습니다. `fmt::Display` 트레잇은 반드시 직접 구현해야합니다.

```rust
// 이 구조체는 `fmt::Display`로 출력할 수 없으며,
// `fmt::Debug`로도 출력할 수 없습니다.
struct UnPrintable(i32);

// 다음 `derive` 속성은 이 구조체가 `fmt::Debug`로 출력될 수 있도록
// 구현체를 자동으로 생성합니다.
#[derive(Debug)]
struct DebugPrintable(i32);
```

`std` 라이브러리 내 타입은 `{:?}` 로도 출력할 수 있습니다.

```rust,editable
// `Structure` 구조체에 `fmt::Debug` 구현체를 derive 합니다.
// `Structure` 구조체는 `i32` 값 하나를 포함합니다.
#[derive(Debug)]
struct Structure(i32);

// `Structure`를 `Deep` 구조체에 집어넣고,
// `Deep` 구조체도 출력 가능하게 만듭니다.
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // `{:?}` 출력은 `{}`와 비슷합니다.
    println!("1년은 {:?}개월입니다.", 12);
    println!("{1:?} {0:?}는 {actor:?} 이름입니다.",
             "슬레이터(Slater)",
             "크리스찬(Christian)",
             actor="배우");

    // `Structure`는 출력 가능합니다.
    println!("이제 {:?}(을)를 출력할 수 있습니다!", Structure(3));
    
    // `derive`의 문제점은 출력 결과의 형태를 조정할 수 없다는 점입니다.
    // 단순히 `7` 만 출력하려면 어떻게 해야 할까요?
    println!("이제 {:?}(을)를 출력할 수 있습니다!", Deep(Structure(7)));
}
```

`fmt::Debug`를 이용해 출력할 수 없던 것을 출력 가능하게 만들어보았습니다.
단정한 형태의 출력을 원하면 `{:#?}`를 사용해 예쁘게 출력할 수 있습니다.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // 예쁘게 출력하기
    println!("{:#?}", peter);
}
```

출력 형태를 원하는 대로 조정하려면 `fmt::Display`를 직접 구현해야 합니다.

### See also:

[`attributes`][attributes], [`derive`][derive], [`std::fmt`][fmt], [`구조체`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: ../../custom_types/structs.md


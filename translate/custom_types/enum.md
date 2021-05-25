# 열거형

`enum` 키워드는 여러 variant(변종) 중 하나의 값이 될 수 있는 타입을 생성합니다.
구조체의 형태로 유효한 것은 열거형의 variant로도 유효합니다.

```rust,editable
// 웹 이벤트를 분류하는 열거형을 생성합니다.
// 열거형의 이름뿐만 아니라 variant를 어떤 방식으로 지정하는지도 유의해주세요.
// `PageLoad`는 `PageUnload`와 다르며, `KeyPress(char)`와 `Paste(String)` 또한 다릅니다.
// 각각의 variant는 모두 다르고 독립적입니다.
enum WebEvent {
    // 열거형은 종류만 지정할 수도 있으며(`unit-like`),
    PageLoad,
    PageUnload,
    // 튜플 구조체 같은 형태도 가능하고,
    KeyPress(char),
    Paste(String),
    // C언어식 구조체도 가능합니다.
    Click { x: i64, y: i64 },
}

// `WebEvent` 열거형을 인자로 전달받고 아무것도 반환하지 않는
// 함수입니다.
fn inspect(event: WebEvent) {
    match event {
        WebEvent::PageLoad => println!("페이지 로드됨"),
        WebEvent::PageUnload => println!("페이지 언로드됨"),
        // 열거형 값 안의 `c`를 해체합니다.
        WebEvent::KeyPress(c) => println!("'{}' 눌림", c),
        WebEvent::Paste(s) => println!("\"{}\" 붙여넣음", s),
        // `Click`을 `x`, `y`로 해체합니다.
        WebEvent::Click { x, y } => {
            println!("x={}, y={} 지점 클릭됨", x, y);
        },
    }
}

fn main() {
    let pressed = WebEvent::KeyPress('x');
    // 소유권을 갖는 `String`을 생성하기 위해 문자열 슬라이스로 `to_owned()`를 호출합니다.
    let pasted  = WebEvent::Paste("텍스트".to_owned());
    let click   = WebEvent::Click { x: 20, y: 80 };
    let load    = WebEvent::PageLoad;
    let unload  = WebEvent::PageUnload;

    inspect(pressed);
    inspect(pasted);
    inspect(click);
    inspect(load);
    inspect(unload);
}

```

## 타입 별칭

타입 별칭을 사용해, 열거형의 별칭으로 각 variant를 참조할 수 있습니다.
열거형의 이름이 너무 길거나, 오히려 너무 평범해서 이름을 바꾸고 싶을 때 유용합니다.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

// 타입 별칭을 생성합니다.
type Operations = VeryVerboseEnumOfThingsToDoWithNumbers;

fn main() {
    // 길고 불편한 이름 대신 별칭으로 각 variant를 참조합니다.
    let x = Operations::Add;
}
```

여러분이 가장 자주 보게 될 타입 별칭은 `impl` 블록 내 `Self` 별칭입니다.

```rust,editable
enum VeryVerboseEnumOfThingsToDoWithNumbers {
    Add,
    Subtract,
}

impl VeryVerboseEnumOfThingsToDoWithNumbers {
    fn run(&self, x: i32, y: i32) -> i32 {
        match self {
            Self::Add => x + y,
            Self::Subtract => x - y,
        }
    }
}
```

### See also:

[`match`][match], [`fn`][fn], [`String`][str], ["Type alias enum variants" RFC][type_alias_rfc]

[c_struct]: https://en.wikipedia.org/wiki/Struct_(C_programming_language)
[match]: ../flow_control/match.md
[fn]: ../fn.md
[str]: ../std/str.md
[aliasreport]: https://github.com/rust-lang/rust/pull/61682/#issuecomment-502472847
[type_alias_rfc]: https://rust-lang.github.io/rfcs/2338-type-alias-enum-variants.html

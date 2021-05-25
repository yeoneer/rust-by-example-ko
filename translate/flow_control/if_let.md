# if let

열거형을 매칭하는 상황 중, `match`를 사용하기에는 불편한 경우가 있습니다.

```rust
// `Option<i32>` 타입 `optional`를 생성합니다
let optional = Some(7);

match optional {
    Some(i) => {
        println!("대충 긴 문자열, `{:?}`", i);
        // ^ `i`를 해체하기까지, 들여쓰기를
        // 두 번이나 해야 합니다.
    },
    _ => {},
    // ^ `match`는 모든 경우를 처리해야 하기 때문에, 이 부분은 필수적입니다.
    // 하지만 굳이 필요할까요?
};

```

이 사례에는 `if let`이 더 깔끔하며,
다양한 실패 옵션을 지정할 수도 있습니다.

```rust,editable
fn main() {
    // 전부 `Option<i32>` 타입입니다
    let number = Some(7);
    let letter: Option<i32> = None;
    let emoticon: Option<i32> = None;

    // `if let` 구문은 다음과 같이 읽습니다.
    // "만약 `number`가 `Some(i)`로 해체된다면 블록(`{}`)을 평가해라."
    if let Some(i) = number {
        println!("일치합니다! {:?}", i);
    }

    // 실패할 경우를 지정하려면 `else`를 사용합니다.
    if let Some(i) = letter {
        println!("일치합니다! {:?}", i);
    } else {
        // 해체 실패했습니다. 실패했을 경우로 변경합니다.
        println!("일치하지 않는 숫자입니다. 문자를 이용해 주세요!");
    }

    // 변할 가능성이 있는 실패 조건
    let i_like_letters = false;

    if let Some(i) = emoticon {
        println!("일치합니다! {:?}", i);
    // 해체 실패했습니다. `else if` 조건을 평가하여
    // 이 분기를 선택해야 하는지 확인합니다.
    } else if i_like_letters {
        println!("일치하지 않는 숫자입니다. 문자를 이용해 주세요!");
    } else {
        // 조건이 false로 평가되었습니다. 이 분기가 기본값입니다.
        println!("문자는 선호하지 않습니다. 이모티콘을 이용해 주세요!");
    }
}
```

같은 방식으로, `if let`를 사용해 어떤 열거형 값이든 매칭할 수 있습니다.

```rust,editable
// 열거형 예시
enum Foo {
    Bar,
    Baz,
    Qux(u32)
}

fn main() {
    // 변수 예시 생성
    let a = Foo::Bar;
    let b = Foo::Baz;
    let c = Foo::Qux(100);
    
    // Foo::Bar에 매칭되는 변수
    if let Foo::Bar = a {
        println!("a는 foobar입니다");
    }
    
    // 변수 b는 Foo::Bar에 매칭되지 않습니다.
    // 따라서 아무것도 출력되지 않습니다.
    if let Foo::Bar = b {
        println!("b는 foobar입니다");
    }
    
    // 변수 c는 Foo::Qux와 매칭됩니다.
    // Foo::Quax는 이전 예제의 Some()처럼 값을 가지고 있습니다.
    if let Foo::Qux(value) = c {
        println!("c는 {}입니다", value);
    }

    // `if let`에서도 바인딩을 사용할 수 있습니다.
    if let Foo::Qux(value @ 100) = c {
        println!("c는 100입니다");
    }
}
```

`if let`의 또 다른 장점은 매개변수화되지 않은 열거형 variant와 매치할 수 있다는 것입니다. 열거형이 `PartialEq`를 구현하거나 derive하지 않아도 말이죠. 이 경우, 열거형의 인스턴스를 동일시할 수 없으므로 `if Foo::Bar == a`는 컴파일할 수 없지만, `if let`은 가능합니다.

직접 해보시겠나요? `if let`을 사용해 다음 예제를 고쳐보세요.

```rust,editable,ignore,mdbook-runnable
// 이 열거형은 의도적으로 PartialEq를 구현하거나 derive하지 않습니다.
// 따라서 이후의 Foo::Bar == a 비교는 실패합니다.
enum Foo {Bar}

fn main() {
    let a = Foo::Bar;

    // 변수 a는 Foo::Bar와 매칭됩니다
    if Foo::Bar == a {
    // ^-- 컴파일 에러가 나타납니다. `if let`을 사용하세요.
        println!("a는 foobar입니다");
    }
}
```

### See also:

[열거형][enum], [`Option`][option], [RFC][if_let_rfc]

[enum]: ../custom_types/enum.md
[if_let_rfc]: https://github.com/rust-lang/rfcs/pull/160
[option]: ../std/option.md

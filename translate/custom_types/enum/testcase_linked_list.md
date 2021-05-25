# Testcase: 연결 리스트

연결 리스트 구현은 적절한 열거형 사용 예시입니다.

```rust,editable
use crate::List::*;

enum List {
    // Cons: 요소와 다음 노드의 포인터를 감싼 튜플 구조체입니다.
    Cons(u32, Box<List>),
    // Nil: 연결 리스트의 끝을 표시하는 노드입니다.
    Nil,
}

// 열거형에는 메소드를 추가할 수 있습니다.
impl List {
    // 빈 리스트를 생성합니다.
    fn new() -> List {
        // `Nil`의 타입은 `List`입니다.
        Nil
    }

    // 리스트의 소유권을 가져오고, 해당 리스트의 앞에 새 요소를 추가한 리스트를 반환합니다.
    fn prepend(self, elem: u32) -> List {
        // `Cons`의 타입도 마찬가지로 `List`입니다.
        Cons(elem, Box::new(self))
    }

    // 리스트 길이를 반환합니다.
    fn len(&self) -> u32 {
        // `self`가 어떤 variant이냐에 따라 다르게 동작하는 메소드이므로
        // `self`를 매치합니다.
        // `self`는 `&List` 타입이니, `*self`는 `List` 타입입니다.
        // 매치할 때는 참조자 `&T` 타입보다 구체적 타입 `T`가 더 선호됩니다.
        // 러스트 2018 에디션 이후에는 다음 위치에 `self`와 `tail` (ref 없이)
        // 을 작성할 수도 있습니다. 러스트는 &s, ref tail을 추론합니다.
        // https://doc.rust-lang.org/edition-guide/rust-2018/ownership-and-lifetimes/default-match-bindings.html 참고
        match *self {
            // `self`는 borrow 되었기 때문에 다음 노드의 소유권을 얻어올 수 없으니,
            // 참조자를 가져옵니다.
            Cons(_, ref tail) => 1 + tail.len(),
            // 기본 케이스: 빈 리스트의 길이는 0입니다.
            Nil => 0
        }
    }

    // 리스트를 문자열(힙 할당된)로 표현하여 반환합니다.
    fn stringify(&self) -> String {
        match *self {
            Cons(head, ref tail) => {
                // `format!`은 `print!`와 유사하지만,
                // 콘솔에 출력하는 대신 힙 할당된 문자열을 반환합니다.
                format!("{}, {}", head, tail.stringify())
            },
            Nil => {
                format!("Nil")
            },
        }
    }
}

fn main() {
    // 빈 연결 리스트를 생성합니다.
    let mut list = List::new();

    // 몇몇 요소를 덧붙입니다.
    list = list.prepend(1);
    list = list.prepend(2);
    list = list.prepend(3);

    // 리스트의 최종 상태를 표시합니다.
    println!("연결 리스트 길이: {}", list.len());
    println!("{}", list.stringify());
}
```

### See also:

[`Box`][box], [methods][methods]

[box]: ../../std/box.md
[methods]: ../../fn/methods.md

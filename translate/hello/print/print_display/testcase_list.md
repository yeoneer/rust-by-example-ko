# Testcase: List

순차적인 요소들을 처리하는 구조체에 `fmt::Display`를 구현하는 건 까다롭습니다.
각 `write!` 마다 `fmt::Result` 를 생성하는데, 이를 **전부** 알맞게
처리해야하기 때문입니다.
러스트에서 제공하는 `?` 연산자는 이런 경우에 딱 알맞습니다.

`write!`에서 `?` 연산자를 사용한 모습은 다음과 같습니다.

```rust,ignore
// `write!`를 시도하여 에러가 있는지 확인합니다.
// 에러가 발생하면 해당 에러를 반환하고, 발생하지 않으면 계속 진행합니다.
write!(f, "{}", value)?;
```

`Vec` 타입에 `fmt::Display`를 구현하는 것도 `?` 연산자를 사용하면
간단합니다.

```rust,editable
use std::fmt; // `fmt`를 가져옵니다.

// `Vec` 타입을 보관하는 `List` 구조체를 정의합니다.
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // 튜플 인덱싱 문법으로 값을 추출하고
        // `vec`에 대한 참조자를 생성합니다.
        let vec = &self.0;

        write!(f, "[")?;

        // 반복자 `v`로 `vec`을 순회하며 반복 횟수를
        // `count`로 열거합니다.
        for (count, v) in vec.iter().enumerate() {
            // 첫 번째 요소 이외에는 쉼표를 추가합니다.
            // 에러일 경우 반환하기 위해 `?` 연산자를 사용합니다.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // 대괄호를 닫고 fmt::Result 값을 반환합니다.
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```

### 실습

프로그램을 수정해서 각 요소의 인덱스 번호도 출력하도록 만들어보세요. 출력 예시는 다음과 같습니다.

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

### See also:

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`?`][q_mark], [`vec!`][vec]

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md

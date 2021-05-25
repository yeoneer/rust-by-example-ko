# match

러스트는 C 언어의 `switch` 처럼
사용할 수 있는 `match` 패턴 매칭을 제공합니다.
가장 먼저 매칭되는 갈래가 평가되며, 가능성이 있는 모든 값이 다뤄져야 합니다.

```rust,editable
fn main() {
    let number = 13;
    // TODO ^ `number`에 다른 값을 설정해 보세요.

    println!("{}는", number);
    match number {
        // 하나의 값 매칭
        1 => println!("1 입니다!"),
        // 여러 값 매칭
        2 | 3 | 5 | 7 | 11 => println!("소수입니다"),
        // TODO ^ 소수 값 목록에 13을 추가해보세요
        // 포함 범위(inclusive range) 매칭
        13..=19 => println!("10대입니다"),
        // 나머지 경우 처리
        _ => println!("특별한 숫자는 아닙니다"),
        // TODO ^ 위의 모든 경우 처리 갈래를 주석 처리해보세요
    }

    let boolean = true;
    // match도 표현식입니다
    let binary = match boolean {
        // 매치 갈래는 가능성 있는 모든 값을 처리해야 합니다
        false => 0,
        true => 1,
        // TODO ^ 갈래 중 하나를 주석 처리해보세요
    };

    println!("{} -> {}", boolean, binary);
}
```

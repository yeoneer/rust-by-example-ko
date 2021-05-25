# 매치 가드

`match` 갈래 필터링에 **가드(guard)**를 추가할 수 있습니다.

```rust,editable
fn main() {
    let pair = (2, -2);
    // TODO ^ `pair`에 다른 값을 설정해 보세요

    println!("{:?}를 설명합니다", pair);
    match pair {
        (x, y) if x == y => println!("둘이 서로 같습니다"),
        // 여기 ^ `if 조건문` 부분이 매치 가드입니다
        (x, y) if x + y == 0 => println!("둘은 상반 관계입니다!"),
        (x, _) if x % 2 == 1 => println!("첫 번째 값은 홀수입니다"),
        _ => println!("서로 상관없는 값이네요..."),
    }
}
```

단, 컴파일러는 표현식의 모든 가능성이
검사되었는지 임의로 평가하지 않습니다.
따라서 마지막에 `_` 패턴을 반드시 사용해야 합니다.

```rust,editable
fn main() {
    let number: u8 = 4;

    match number {
        i if i == 0 => println!("0"),
        i if i > 0 => println!("0보다 큼"),
        _ => println!("그냥 통과"), // 이 부분은 도달할 수 없어야 합니다
    }
}
```

### See also:

[튜플](../../primitives/tuples.md)

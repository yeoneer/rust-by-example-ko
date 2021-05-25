# loop

러스트에선 `loop` 키워드로 무한 반복을 명시할 수 있습니다.

`break` 구문으로 언제든지 반복을 끝낼 수 있습니다.
`continue` 구문은 현 회차의 나머지를 생략하고,
새로운 회차를 시작합니다.

```rust,editable
fn main() {
    let mut count = 0u32;

    println!("무한 카운트 시작!");

    // 무한 반복
    loop {
        count += 1;

        if count == 3 {
            println!("셋");

            // 이번 회차의 나머지 생략
            continue;
        }

        println!("{}", count);

        if count == 5 {
            println!("이 정도면 충분하겠네요");

            // 반복 종료
            break;
        }
    }
}
```
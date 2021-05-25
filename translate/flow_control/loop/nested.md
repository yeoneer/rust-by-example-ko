# 중첩, 라벨

중첩된 반복 내에서 `break`, `continue`로 외부 반복문을 제어하는 것도 가능합니다.
이 경우, 반복문에는 어떤 `'label` 이 어노테이션되어있어야 하며,
해당 라벨을  `break`/`continue` 구문에 전달해야 합니다.

```rust,editable
#![allow(unreachable_code)]

fn main() {
    'outer: loop {
        println!("바깥쪽 반복문 진입");

        'inner: loop {
            println!("안쪽 반복문 진입");

            // 이 break 구문은 안쪽 반복문을 종료합니다
            //break;

            // 이 break 구문은 바깥쪽 반복문을 종료합니다
            break 'outer;
        }

        println!("이 부분은 실행될 일이 없습니다");
    }

    println!("바깥쪽 반복문 종료됨");
}
```
# 반복문에서 반환하기

`loop`는 어떤 작업에 성공할 때까지 재시도하는 용도로 사용되기도 합니다.
해당 작업이 어떠한 값을 반환하고, 이후의 코드에서 사용할 수 있도록
값을 전달해야 할 경우, `break` 구문 뒤에 값을 작성하면
`loop` 표현식이 해당 값을 반환합니다.

```rust,editable
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    assert_eq!(result, 20);
}
```

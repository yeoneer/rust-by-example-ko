# 포인터/참조자

포인터의 경우, `C` 같은 언어와는 사용 개념이 다르므로
해체(destructuring)와 역참조(dereferencing)를
구별해야 합니다.

* 역참조는 `*`를 사용합니다
* 해체는 `&`, `ref`, `ref mut`를 사용합니다

```rust,editable
fn main() {
    // `i32` 타입의 참조자를 할당합니다.
    // `&`는 참조자가 대입됨을 나타냅니다.
    let reference = &4;

    match reference {
        // `reference`를 `&val`에 매치되는 패턴으로 비교하면
        // 다음과 같습니다:
        // `&i32`
        // `&val`
        // ^ 대응되는 `&i32`의 `&` 가 빠지면 `val`에 대입될
        // `i32`만 남는 것을 확인할 수 있습니다.
        &val => println!("해체로 얻은 값: {:?}", val),
    }

    // 매칭하기 전에 역참조하면 `&`를 회피할 수 있습니다.
    match *reference {
        val => println!("역참조로 얻은 값: {:?}", val),
    }

    // 처음부터 참조가 아닌 경우엔 어떨까요?
    // `reference`는 우변이 참조자였으니 `&` 였지만,
    // 이번엔 우변이 참조자가 아닙니다.
    let _not_a_reference = 3;

    // 러스트는 이 용도로 `ref`를 제공합니다.
    // `ref`는 대입문을 수정해서, 요소에 대한 참조자를
    // 생성하고 대입합니다.
    let ref _is_a_reference = 3;

    // 참조 없이 두 값을 정의하고
    // `ref`, `ref mut`으로 참조자를 얻어옵니다.
    let value = 5;
    let mut mut_value = 6;

    // `ref` 키워드로 참조자를 생성합니다.
    match value {
        ref r => println!("값의 참조자: {:?}", r),
    }

    // `ref mut` 사용 방법도 비슷합니다.
    match mut_value {
        ref mut m => {
            // 참조자를 얻어옵니다.
            // 역참조했으므로 값을 더할 수 있습니다.
            *m += 10;
            println!("10을 더했습니다. `mut_value`: {:?}", m);
        },
    }
}
```

### See also:

[The ref pattern](../../../scope/borrow/ref.md)

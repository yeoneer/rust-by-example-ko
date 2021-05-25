# 변수 바인딩

러스트는 정적 타이핑으로 타입 안전성을 보장합니다.
따라서 변수 바인딩 선언 시 타입 어노테이션을 작성할 수 있습니다.
하지만 대부분의 경우는 컴파일러가 문맥에 맞게 타입을 추론하기 때문에,
어노테이션 작성 부담은 크지 않습니다.

리터럴 등의 값을 변수에 바인딩할 때에는 `let` 바인딩을 사용합니다.

```rust,editable
fn main() {
    let an_integer = 1u32;
    let a_boolean = true;
    let unit = ();

    // `an_integer`를 `copied_integer`로 복사합니다.
    let copied_integer = an_integer;

    println!("정수: {:?}", copied_integer);
    println!("boolean: {:?}", a_boolean);
    println!(")유닛 값을 소개합니다: {:?}", unit);

    // 컴파일러는 사용되지 않은 변수 바인딩에 `unused variable` 경고를 표시합니다.
    // 변수명 앞에 밑줄(`_`, 언더스코어)을 추가하면 해당 경고를 잠재울 수 있습니다.
    let _unused_variable = 3u32;

    let noisy_unused_variable = 2u32;
    // 고쳐주세요! ^ 앞에 밑줄을 추가해 경고가 나타나지 않도록 하세요
}
```

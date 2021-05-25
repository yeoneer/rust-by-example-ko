# `TryFrom`, `TryInto`

[`From`, `Into`][from-into]와 마찬가지로,
[`TryFrom`], [`TryInto`]은 형변환용 제네릭 트레잇입니다.
다만 `From`/`Into` 와는 다르게, `TryFrom`/`TryInto` 트레잇은
실패할 가능성이 있는 변환에 사용됩니다(따라서 [`Result`]를 반환합니다).

[from-into]: from_into.html
[`TryFrom`]: https://doc.rust-lang.org/std/convert/trait.TryFrom.html
[`TryInto`]: https://doc.rust-lang.org/std/convert/trait.TryInto.html
[`Result`]: https://doc.rust-lang.org/std/result/enum.Result.html

```rust,editable
use std::convert::TryFrom;
use std::convert::TryInto;

#[derive(Debug, PartialEq)]
struct EvenNumber(i32); // 짝수

impl TryFrom<i32> for EvenNumber {
    type Error = ();

    fn try_from(value: i32) -> Result<Self, Self::Error> {
        if value % 2 == 0 {
            Ok(EvenNumber(value))
        } else {
            Err(())
        }
    }
}

fn main() {
    // TryFrom

    assert_eq!(EvenNumber::try_from(8), Ok(EvenNumber(8)));
    assert_eq!(EvenNumber::try_from(5), Err(()));

    // TryInto

    let result: Result<EvenNumber, ()> = 8i32.try_into();
    assert_eq!(result, Ok(EvenNumber(8)));
    let result: Result<EvenNumber, ()> = 5i32.try_into();
    assert_eq!(result, Err(()));
}
```

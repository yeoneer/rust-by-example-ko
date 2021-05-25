# 형변환

기본 타입은 서로 간에 [형변환(Casting)][casting]할 수 있습니다.

러스트에서 커스텀 타입(`struct`, `enum` 등) 간
형변환(Conversion)은 [트레잇][traits]을 사용합니다.
일반적인 형변환은 [`From`], [`Into`] 트레잇을 이용하며,
자주 사용되는 `String` 형변환은 별도의 방법이
특별히 제공됩니다.

[casting]: types/cast.md
[traits]: trait.md
[`From`]: https://doc.rust-lang.org/std/convert/trait.From.html
[`Into`]: https://doc.rust-lang.org/std/convert/trait.Into.html

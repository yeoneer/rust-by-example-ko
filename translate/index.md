# 예제로 배우는 Rust

[Rust][rust]는 안정성, 속도, 동시성에 초점을 둔 모던 프로그래밍 언어입니다.
가비지 컬렉션 없이 메모리 안전성을 보장함으로써 이 모든 목표를 달성합니다.

예제로 배우는 Rust(Rust by Example, RBE)는 직접 실행해볼 수 있는 예제들을 모아 러스트의 다양한 개념과 표준 라이브러리를 설명합니다. 더 많은 예제를 원하신다면 [직접 러스트를 설치해서][install], [공식 문서][std]를 살펴보세요. 궁금한 점이 있다면 [이 사이트의 소스 코드][home]를 직접 확인하실 수도 있습니다.

이제 시작해봅시다!

- [Hello World](hello.md) - 시작은 언제나의 Hello World 프로그램입니다.

- [기본 요소](primitives.md) - 부호 정수, 부호 없는 정수 등의 기본 요소를 배웁니다.

- [커스텀 타입](custom_types.md) - `struct`, `enum`

- [변수 바인딩](variable_bindings.md) - 가변 변수 바인딩, 스코프, 변수 가리기

- [타입](types.md) - 타입 정의 및 변환을 배웁니다.

- [형변환](conversion.md)

- [표현식](expression.md)

- [흐름 제어](flow_control.md) - `if`/`else`, `for` 등

- [함수](fn.md) - 메소드, 클로저, 고차 함수를 배웁니다.

- [모듈](mod.md) - 모듈을 이용한 코드 조직화

- [Crate(크레이트)](crates.md) - 크레이트는 러스트의 컴파일 단위입니다. 라이브러리 제작을 배웁니다.

- [Cargo](cargo.md) - 러스트 공식 패키지 관리 툴 기본 기능을 살펴봅니다.

- [Attributes](attribute.md) - An attribute is metadata applied to some module, crate or item.

- [제네릭](generics.md) - 다양한 타입의 인자로 작동하는 함수나 데이터 형식을 작성하는 방법을 배웁니다.

- [범위 규칙](scope.md) - 범위는 소유권, borrowing, 라이프타임에서 중요한 역할을 합니다.

- [Trait(트레잇)](trait.md) - 트레잇은 `Self` 라는 알 수 없는 타입에 정의된 메소드의 집합입니다.

- [매크로](macros.md)

- [에러 처리](error.md) - 러스트의 에러 처리 방식을 배웁니다.

- [표준 라이브러리 타입](std.md) - `std` 라이브러리에서 제공하는 커스텀 타입의 일부를 알아봅니다.

- [Std misc](std_misc.md) - 파일 처리, 스레드용 커스텀 타입도 있답니다.

- [테스트](testing.md) - 러스트의 온갖 종류 테스트

- [Unsafe 연산](unsafe.md)

- [호환성](compatibility.md)

- [개발 외](meta.md) - 문서화, 벤치마킹

[rust]: https://www.rust-lang.org/
[install]: https://www.rust-lang.org/tools/install
[std]: https://doc.rust-lang.org/std/
[home]: https://github.com/rust-lang/rust-by-example

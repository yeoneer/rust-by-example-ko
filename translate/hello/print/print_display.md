# Display

`fmt::Debug`로는 간결하고 깔끔한 출력을 만들기 어렵습니다.
출력 형태를 원하는대로 바꾸기 위해선 [`fmt::Display`][fmt](출력 시 `{}`로 표시)를 직접 구현해야 합니다.
구현 방법은 다음과 같습니다.

```rust
// `use` 키워드로`fmt` 모듈을 가져옵니다.
use std::fmt;

// `fmt::Display`를 구현할 구조체를 정의합니다.
// `Structure`는 `i32` 값을 갖는 튜플 구조체입니다.
struct Structure(i32);

// `{}` 표시자는 `fmt::Display` 트레잇을 구현하는
// 타입으로만 사용할 수 있습니다.
impl fmt::Display for Structure {
    // Display 트레잇의 정확한 시그니처에선 `fmt`를 사용합니다
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // 제공된 출력 스트림 `f`에 첫 번째 요소를 작성합니다.
        // 반환하는 `fmt::Result`는 연산의 성공 여부를 나타냅니다.
        // `write!` 사용 문법은 `println!`과 굉장히 유사하다는 점을
        // 기억해두세요.
        write!(f, "{}", self.0)
    }
}
```

`fmt::Display`는 `fmt::Debug`보다 깔끔합니다. 하지만, 오히려 깔끔하기 때문에  `std` 라이브러리는 `fmt::Display` 기본 구현을 제공하지 않습니다.
타입의 출력 형태를 정하기가 애매하기 때문입니다.
예를 들어, 만약 `std` 라이브러리에서 `Vec<T>` 타입의 출력을 구현한다면, 어떤 형태로 출력되도록 구현해야 할까요? 다음 두 가지 중 하나일까요?

* `Vec<path>`: `/:/etc:/home/username:/bin` (`:`로 구분)
* `Vec<number>`: `1,2,3` (`,`로 구분)

모든 타입에 어울리는 이상적인 형태는 존재하지 않습니다.
따라서 `std` 라이브러리는 함부로 `Vec<T>` 등의 기본 제네릭 컨테이너에 `fmt::Display`를 구현하지 않습니다.
기본 제네릭 컨테이너에는 `fmt::Debug`를 사용해야 합니다.

표준 라이브러리의 기본 제네릭 컨테이너가 **아닌**,
새로 만든 **컨테이너** 타입에는 문제 없이 `fmt::Display`를 구현할 수 있습니다.

```rust,editable
use std::fmt; // `fmt`를 가져옵니다.

// 두 숫자를 보관하는 구조체입니다. `Display` 결과와 비교하기 위해
// `Debug`를 derive합니다.
#[derive(Debug)]
struct MinMax(i64, i64);

// `MinMax`에 `Display`를 구현합니다.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // `self.숫자`는 각 위치의 데이터를 가리킵니다.
        write!(f, "({}, {})", self.0, self.1)
    }
}

// 비교를 위해, 필드에 이름을 붙인 구조체를 정의합니다.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// 마찬가지로 `Point2D`에도 `Display`를 구현합니다.
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // `x`, `y`만 표시하도록 합니다.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("구조체 비교");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("큰 범위는 {big}이며, 작은 범위는 {small}입니다.",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Point 비교");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // 다음 줄은 작동하지 않습니다. `Debug`, `Display`를 모두 구현하더라도
    // `{:b}`는 `fmt::Binary`가 구현되어야 작동하기 때문입니다.
    // println!("Point2D를 이진법으로 나타내면 어떤 모습일까요? {:b}?", point);
}
```

`fmt::Display`를 구현한다고 해서 만사가 해결되는건 아닙니다.
만약 바이너리 출력을 사용하려면, `fmt::Binary`를 구현해야합니다.
바이너리 이외에도 각각 따로 구현해야하는 `std::fmt` [`트레잇`][traits]은 여럿 있습니다.
(자세한 내용은 [`std::fmt`][fmt]를 찾아보세요.)

### 실습

앞선 예제에서 어떤 출력이 나오는지 확인해보았다면, `Point2D` 구조체 정의 예시 삼아
`Complex` 구조체를 추가해보세요. 동일한 방식으로 출력하여 다음과 같은 결과가 나와야합니다.

```txt
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
```

### See also:

[`derive`][derive], [`std::fmt`][fmt], [`매크로`][macros], [`구조체`][structs],
[`트레잇`][traits], [`use`][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[use]: ../../mod/use.md

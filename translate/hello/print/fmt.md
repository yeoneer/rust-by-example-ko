# 포맷팅

앞서 봤듯, 포맷팅은 **포맷 문자열(format string)** 로 명시합니다.

* `format!("{}", foo)` -> `"3735928559"`
* `format!("0x{:X}", foo)` ->
  [`"0xDEADBEEF"`][deadbeef]
* `format!("0o{:o}", foo)` -> `"0o33653337357"`

똑같은 `foo` 변수를 **인수 형식(argument type)** 에 따라 다르게 포맷팅할 수 있습니다.
각각 `X`, `o`, **명시되지 않은** 인수 형식을 사용했습니다.

포맷팅 기능은 여러 트레잇으로 구현되어 있으며, 각각의 트레잇이 인수 형식에 하나씩 대응합니다.
가장 보편적인 포맷팅 트레잇은 `Display` 트레잇입니다.
`Display` 트레잇은 명시되지 않은 인수 형식(`{}`)을 처리합니다.

```rust,editable
use std::fmt::{self, Formatter, Display};

struct City {
    name: &'static str,
    // 위도(Latitude)
    lat: f32,
    // 경도(Longitude)
    lon: f32,
}

impl Display for City {
    // `f`는 버퍼입니다. fmt 메소드는 포맷 스트링을 `f` 버퍼에 작성해야 합니다.
    fn fmt(&self, f: &mut Formatter) -> fmt::Result {
        let lat_c = if self.lat >= 0.0 { 'N' } else { 'S' };
        let lon_c = if self.lon >= 0.0 { 'E' } else { 'W' };

        // `write!`은 `format!`과 비슷하지만, 첫 번째 인수인 버퍼에
        // 포맷 스트링을 작성한다는 차이점이 있습니다.
        write!(f, "{}: {:.3}°{} {:.3}°{}",
               self.name, self.lat.abs(), lat_c, self.lon.abs(), lon_c)
    }
}

#[derive(Debug)]
struct Color {
    red: u8,
    green: u8,
    blue: u8,
}

fn main() {
    for city in [
        City { name: "더블린", lat: 53.347778, lon: -6.259722 },
        City { name: "오슬로", lat: 59.95, lon: 10.75 },
        City { name: "밴쿠버", lat: 49.25, lon: -123.1 },
    ].iter() {
        println!("{}", *city);
    }
    for color in [
        Color { red: 128, green: 255, blue: 90 },
        Color { red: 0, green: 3, blue: 254 },
        Color { red: 0, green: 0, blue: 0 },
    ].iter() {
        // fmt::Display를 구현하고 나면 이 부분을 {}로 변경하세요.
        println!("{:?}", *color);
    }
}
```

더 자세히 알아보고 싶다면 [전체 포맷팅 트레잇 목록][fmt_traits]이나
[`std::fmt`][fmt] 문서에서 포맷팅 인수 형식을 살펴볼 수 있습니다.

### 실습

앞선 코드의 `Color` 구조체에 `fmt::Display` 트레잇을 구현하여
출력 결과가 다음과 같이 나타나도록 만들어보세요.

```text
RGB (128, 255, 90) 0x80FF5A
RGB (0, 3, 254) 0x0003FE
RGB (0, 0, 0) 0x000000
```

막힐 때를 위해 힌트를 드리겠습니다.

* [하나의 색깔을 여러 번 표시하는 방법][named_parameters],
* `:02`를 사용하면 [2칸 내 공백에 0을 채울 수 있습니다(Zero Padding).][fmt_width]

### See also:

[`std::fmt`][fmt]

[named_parameters]: https://doc.rust-lang.org/std/fmt/#named-parameters
[deadbeef]: https://en.wikipedia.org/wiki/Deadbeef#Magic_debug_values
[fmt]: https://doc.rust-lang.org/std/fmt/
[fmt_traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[fmt_width]: https://doc.rust-lang.org/std/fmt/#width

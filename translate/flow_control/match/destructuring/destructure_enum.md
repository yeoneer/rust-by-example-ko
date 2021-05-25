# 열거형

`enum` 해체도 비슷합니다.

```rust,editable
// 이 `allow`는 하나의 variant만 사용할 경우
// 나타나는 경고를 억제합니다.
#[allow(dead_code)]
enum Color {
    // 이 3개는 이름만 존재합니다
    Red,
    Blue,
    Green,
    // `u32` 튜플을 색상 모델 이름으로 묶습니다.
    RGB(u32, u32, u32),
    HSV(u32, u32, u32),
    HSL(u32, u32, u32),
    CMY(u32, u32, u32),
    CMYK(u32, u32, u32, u32),
}

fn main() {
    let color = Color::RGB(122, 17, 40);
    // TODO ^ `color`에 다른 variant를 설정해 보세요

    println!("어떤 색상인가요?");
    // 매치에서 열거형을 해체할 수 있습니다.
    match color {
        Color::Red   => println!("빨간색입니다!"),
        Color::Blue  => println!("파란색입니다!"),
        Color::Green => println!("초록색입니다!"),
        Color::RGB(r, g, b) =>
            println!("빨간색: {}, 초록색: {}, 파란색: {}!", r, g, b),
        Color::HSV(h, s, v) =>
            println!("색상(Hue): {}, 채도(Saturation): {}, 명도(Value): {}!", h, s, v),
        Color::HSL(h, s, l) =>
            println!("색상(Hue): {}, 채도(Saturation): {}, 명도(Lightness): {}!", h, s, l),
        Color::CMY(c, m, y) =>
            println!("Cyan: {}, Magenta: {}, Yellow: {}!", c, m, y),
        Color::CMYK(c, m, y, k) =>
            println!("Cyan: {}, Magenta: {}, Yellow: {}, Key(Black): {}!",
                c, m, y, k),
        // 모든 variant가 검사되었으므로 더 이상의 갈래가 필요하지 않습니다
    }
}
```

### See also:

[`#[allow(...)]`][allow], [색상 모델][color_models], [열거형(`enum`)][enum]

[allow]: ../../../attribute/unused.md
[color_models]: https://en.wikipedia.org/wiki/Color_model
[enum]: ../../../custom_types/enum.md

# 구조체

`struct` 해체도 비슷합니다.

```rust,editable
fn main() {
    struct Foo {
        x: (u32, u32),
        y: u32,
    }

    // 구조체 내 값을 변경하면 어떻게 되는지 확인해보세요
    let foo = Foo { x: (1, 2), y: 3 };

    match foo {
        Foo { x: (1, b), y } => println!("x의 첫 번째 값 = 1, b = {},  y = {} ", b, y),

        // 구조체를 해체하고 변수의 이름을 다시 지을 수도 있습니다.
        // 순서는 중요하지 않습니다.
        Foo { y: 2, x: i } => println!("y is 2, i = {:?}", i),

        // 일부 변수를 무시할 수도 있습니다:
        Foo { y, .. } => println!("y = {}, x는 신경 쓰지 않습니다", y),
        // 다음은 오류가 발생합니다. 패턴에 `x` 필드가 언급되지 않았습니다.
        //Foo { y } => println!("y = {}", y),
    }
}
```

### See also:

[구조체](../../../custom_types/structs.md)

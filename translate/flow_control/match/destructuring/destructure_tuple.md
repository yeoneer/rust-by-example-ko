# 튜플

`match`에서, 튜플은 다음과 같이 해체할 수 있습니다.

```rust,editable
fn main() {
    let triple = (0, -2, 3);
    // TODO ^ `triple`에 다른 값을 넣어 보세요

    println!("{:?}", triple);
    // 매치에서 튜플을 해체할 수 있습니다.
    match triple {
        // 두 번째, 세 번째 요소를 해체합니다
        (0, y, z) => println!("첫 번째는 `0`, `y`는 {:?}, `z`는 {:?}", y, z),
        (1, ..)  => println!("첫 번째는 `1`, 나머지는 상관없음"),
        // `..`는 튜플의 나머지를 무시하는 데 사용합니다
        _      => println!("뭐든지 상관없음"),
        // `_`는 값을 변수에 바인딩하지 않음을 의미합니다
    }
}
```

### See also:

[튜플](../../../primitives/tuples.md)

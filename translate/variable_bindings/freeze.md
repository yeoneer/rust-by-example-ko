# 변수 동결

가변 변수를 동일한 이름의 불변 변수로 바인딩하면 데이터를 **동결**(freeze)할 수 있습니다.
동결된 데이터는 불변 바인딩이 스코프를 벗어나기 전까진 수정할 수 없습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let mut _mutable_integer = 7i32;

    {
        // 불변 `_mutable_integer`로 가리기
        let _mutable_integer = _mutable_integer;

        // 에러! `_mutable_integer`는 이 스코프에서 동결되었습니다.
        _mutable_integer = 50;
        // 고쳐주세요! ^ 이 줄을 주석 처리해주세요.

        // `_mutable_integer`가 스코프를 벗어남
    }

    // 문제없음! `_mutable_integer`는 이 스코프에서 동결되어있지 않습니다.
    _mutable_integer = 3;
}
```

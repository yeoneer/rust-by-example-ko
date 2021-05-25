# 리터럴, 연산자

정수 `1`, 부동 소수점 `1.2`, 문자 `'a'`, 문자열 `"abc"`, boolean `true`,
유닛 타입 `()`은 리터럴로 표현할 수 있습니다.

정수는 `0x`, `0o`, `0b` 접두사를 사용해 각각 16진수, 8진수, 2진수로
표기할 수 있습니다.

숫자 리터럴에 언더스코어(`_`)를 추가하여 가독성을 높일 수도 있습니다.
`1_000`은 `1000`과 같고, `0.000_001`은 `0.000001`와 같습니다.

<!-- 원문: We need to tell the compiler the type of the literals we use. -->
원하는 타입의 리터럴을 사용하려면 컴파일러에게 타입을 알려주어야 합니다.
이번에는 부호 없는 32비트 정수 리터럴을 `u32` 접미사로 표시하고,
부호 있는 32비트 정수 리터럴을 `i32` 접미사로 표시하겠습니다.

[러스트에서 사용 가능한 연산자와 연산자 우선 순위][rust op-prec]는
다른 [C언어계 언어(C-like languages)][op-prec]와 유사합니다.

```rust,editable
fn main() {
    // 정수 덧셈
    println!("1 + 2 = {}", 1u32 + 2);

    // 정수 뺄셈
    println!("1 - 2 = {}", 1i32 - 2);
    // TODO ^  `1i32`를 `1u32`로 바꿔보면 타입이 중요한 이유를 알 수 있습니다.

    // boolean 논리 연산
    println!("true AND false = {}", true && false);
    println!("true OR false = {}", true || false);
    println!("NOT true = {}", !true);

    // 비트 연산
    println!("0011 AND 0101 = {:04b}", 0b0011u32 & 0b0101);
    println!("0011 OR 0101 = {:04b}", 0b0011u32 | 0b0101);
    println!("0011 XOR 0101 = {:04b}", 0b0011u32 ^ 0b0101);
    println!("1 << 5 = {}", 1u32 << 5);
    println!("0x80 >> 2 = 0x{:x}", 0x80u32 >> 2);

    // 언더스코어를 사용해 가독성을 높였습니다.
    println!("백만을 숫자로 쓰면 {}입니다", 1_000_000u32);
}
```

[rust op-prec]: https://doc.rust-lang.org/reference/expressions.html#expression-precedence
[op-prec]: https://en.wikipedia.org/wiki/Operator_precedence#Programming_languages

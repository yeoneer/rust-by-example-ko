# 함수

함수는 `fn` 키워드로 선언합니다.
인수에는 변수처럼 타입을 명시합니다.
함수가 값을 반환하는 경우, `->` 화살표 뒤에 반환 타입을 반드시 명시해야 합니다.

함수의 마지막 표현식은 반환 값으로 사용됩니다.
또는 `return` 구문으로 함수에서 일찍 값을 반환할 수 있습니다.
`return` 구문은 함수 내 `if` 구문과 반복문에서도 사용 가능합니다.

함수를 사용해 FizzBuzz를 구현해봅시다!

```rust,editable
// C/C++과는 달리, 함수 정의 순서에는 제한이 없습니다
fn main() {
    // 여기서 함수를 사용하고, 나중에 정의할 수 있죠.
    fizzbuzz_to(100);
}

// boolean 값을 반환하는 함수
fn is_divisible_by(lhs: u32, rhs: u32) -> bool {
    // Corner case, early return
    if rhs == 0 {
        return false;
    }

    // 다음은 표현식입니다. 따라서 `return` 키워드는 불필요합니다.
    lhs % rhs == 0
}

// 값을 반환하지 '않는' 함수 (실제로는 유닛 타입 `()`를 반환함)
fn fizzbuzz(n: u32) -> () {
    if is_divisible_by(n, 15) {
        println!("fizzbuzz");
    } else if is_divisible_by(n, 3) {
        println!("fizz");
    } else if is_divisible_by(n, 5) {
        println!("buzz");
    } else {
        println!("{}", n);
    }
}

// 함수가 `()`를 반환하는 경우,
// 반환 타입은 시그니처에서 생략 가능합니다.
fn fizzbuzz_to(n: u32) {
    for n in 1..n + 1 {
        fizzbuzz(n);
    }
}
```

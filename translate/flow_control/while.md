# while

`while` 키워드는 조건이 참인 동안 반복합니다.

`while` 반복문으로 [FizzBuzz][fizzbuzz] 문제를 구현해보죠.

```rust,editable
fn main() {
    // 카운터 변수
    let mut n = 1;

    // `n`이 101 미만인 동안 반복
    while n < 101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }

        // 카운터 증가
        n += 1;
    }
}
```

[fizzbuzz]: https://en.wikipedia.org/wiki/Fizz_buzz

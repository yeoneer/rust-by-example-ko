# for 반복문

## 범위 표기법으로 for 반복문 사용하기

`for in` 구문은 `Iterator`를 통해 순회합니다.
반복자(iterator)를 만드는 가장 쉬운 방법은 범위 표기법을 사용하는 겁니다.
`a..b` 범위 표기법은 `a`(포함)부터 `b`(제외)까지,
한 단계씩 값이 생성됩니다.

FizzBuzz 문제를 `while` 대신 `for` 반복문으로 구현해보겠습니다.

```rust,editable
fn main() {
    // `n`은 각 회차에 따라 1, 2, ..., 100이 됩니다
    for n in 1..101 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

범위의 양쪽 끝을 모두 포함하려면 `a..=b`를 사용합니다.
위 예제를 `a..=b` 표기법을 사용해 작성하면 다음과 같습니다.

```rust,editable
fn main() {
    // `n`은 각 회차에 따라 1, 2, ..., 100이 됩니다
    for n in 1..=100 {
        if n % 15 == 0 {
            println!("fizzbuzz");
        } else if n % 3 == 0 {
            println!("fizz");
        } else if n % 5 == 0 {
            println!("buzz");
        } else {
            println!("{}", n);
        }
    }
}
```

## 반복자(Iterator)로 for 반복문 사용하기

`for in` 구문은 `Iterator`와 사용할 수 있습니다.
[Iterator][iter] 트레잇 부분에서 다뤘듯, `for` 반복문은
기본적으로 `into_iter` 함수를 컬렉션에 적용합니다.
물론, `into_iter` 만이 컬렉션을 반복자로 변환하는 유일한 방법은 아닙니다.

`into_iter`, `iter`, `iter_mut`는
모두 컬렉션을 반복자로 변환하며,
데이터를 각각의 관점으로 제공합니다.

* `iter` - 컬렉션의 각 요소를 borrow 합니다.
  컬렉션을 건드리지 않으므로, 반복문 이후에도 사용할 수 있습니다.

```rust,editable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter() {
        match name {
            &"Ferris" => println!("이 중에 러스트 사용자가 있다!"),
            // TODO ^ `&`를 지우고 "Ferris"로만 매칭해보세요
            _ => println!("안녕, {}", name),
        }
    }
    
    println!("names: {:?}", names);
}
```

* `into_iter` - 컬렉션을 소비하여 각 회차에 정확한 데이터를 가져옵니다.
  데이터가 반복문 내로 '이동'되므로 컬렉션을 소비하고 나면
  이후에는 사용할 수 없습니다.

```rust,editable,ignore,mdbook-runnable
fn main() {
    let names = vec!["Bob", "Frank", "Ferris"];

    for name in names.into_iter() {
        match name {
            "Ferris" => println!("이 중에 러스트 사용자가 있다!"),
            _ => println!("안녕, {}", name),
        }
    }
    
    println!("names: {:?}", names);
    // 고쳐주세요! ^ 이 줄을 주석 처리해주세요
}
```

* `iter_mut` - 컬렉션의 각 요소를 변경 가능하게 borrow 합니다.
  컬렉션을 수정할 수 있습니다.

```rust,editable
fn main() {
    let mut names = vec!["Bob", "Frank", "Ferris"];

    for name in names.iter_mut() {
        *name = match name {
            &mut "Ferris" => "이 중에 러스트 사용자가 있다!",
            _ => "안녕",
        }
    }

    println!("names: {:?}", names);
}
```

앞선 코드 예제에서는 `match` 가지의 타입을 주목해주세요.
각 종류의 주요 차이점입니다.
당연하지만, 여러 종류가 존재한다는 것은 종류마다 할 수 있는 일이 다르다는 의미입니다.

### See also:

[Iterator][iter]

[iter]: ../trait/iter.md

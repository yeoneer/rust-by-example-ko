# 튜플

튜플은 다양한 타입 값의 집합입니다.
튜플은 괄호를 사용해 생성하며, 각각의 튜플은 `(T1, T2, ...)`
(`T1`, `T2`은 구성 요소의 타입) 타입 시그니처 타입의 값입니다.
튜플은 여러 값을 포함할 수 있으므로 함수에서 튜플을 이용해 여러 값을 반환할 수도 있습니다.

```rust,editable
// 튜플은 함수 인수 및 반환 값으로 사용할 수 있습니다.
fn reverse(pair: (i32, bool)) -> (bool, i32) {
    // `let` 구문으로 튜플의 구성 요소를 변수에 바인딩합니다.
    let (integer, boolean) = pair;

    (boolean, integer)
}

// 실습용 구조체입니다.
#[derive(Debug)]
struct Matrix(f32, f32, f32, f32);

fn main() {
    // 다양한 타입이 모인 튜플
    let long_tuple = (1u8, 2u16, 3u32, 4u64,
                      -1i8, -2i16, -3i32, -4i64,
                      0.1f32, 0.2f64,
                      'a', true);

    // 튜플 내 값은 튜플 인덱싱을 사용해 추출할 수 있습니다
    println!("long tuple 첫 번째 값: {}", long_tuple.0);
    println!("long tuple 두 번째 값: {}", long_tuple.1);

    // 튜플이 튜플의 구성요소가 될 수도 있습니다.
    let tuple_of_tuples = ((1u8, 2u16, 2u32), (4u64, -1i8), -2i16);

    // 튜플은 출력 가능합니다.
    println!("튜플로 만든 튜플: {:?}", tuple_of_tuples);
    
    // 하지만 긴 튜플은 출력할 수 없습니다.
    // let too_long_tuple = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13);
    // println!("너무 긴 튜플: {:?}", too_long_tuple);
    // TODO ^ 위 두 줄을 주석 해제하여 어떤 컴파일러 에러가 나타나는지 확인해보세요.

    let pair = (1, true);
    println!("쌍은 {:?}입니다.", pair);

    println!("뒤집은 쌍은 {:?}입니다.", reverse(pair));

    // 요소가 하나뿐인 튜플을 생성할 땐 괄호로 둘러싸인 리터럴과 구별하기 위해
    // 반드시 쉼표를 작성해야 합니다.
    println!("{:?}는 요소가 하나인 튜플입니다.", (5u32,));
    println!("{:?}는 그냥 숫자입니다.", (5u32));

    // 튜플을 해체하여 바인딩을 생성할 수 있습니다.
    let tuple = (1, "hello", 4.5, true);

    let (a, b, c, d) = tuple;
    println!("{:?}, {:?}, {:?}, {:?}", a, b, c, d);

    let matrix = Matrix(1.1, 1.2, 2.1, 2.2);
    println!("{:?}", matrix);

}
```

### 실습

 1. **복습**: 앞선 예제의 `Matrix` 구조체에 `fmt::Display` 트레잇을 구현해보세요.
    출력 부분의 Debug 포맷팅(`{:?}`)을 Display 포맷팅(`{}`)으로 변경했을 때
    다음과 같은 결과가 출력되어야 합니다.

    ```text
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    ```

    필요하다면, 이전 [Display 출력][print_display] 예제를 참고하세요.
 2. `reverse` 함수를 참고자료 삼아, matrix(행렬)를 인수로 받아
    두 개의 요소를 교환하여 반환하는 `transpose` 함수를 추가해보세요.
    예시는 다음과 같습니다.

    ```rust,ignore
    println!("Matrix:\n{}", matrix);
    println!("Transpose:\n{}", transpose(matrix));
    ```

    다음은 출력 결과입니다.

    ```text
    Matrix:
    ( 1.1 1.2 )
    ( 2.1 2.2 )
    Transpose:
    ( 1.1 2.1 )
    ( 1.2 2.2 )
    ```

[print_display]: ../hello/print/print_display.md

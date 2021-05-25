# Hello World

다음은 러스트로 작성한 Hello World 프로그램 소스 코드입니다.

```rust,editable
// 이건 주석입니다. 주석은 프로그램에 영향을 주지 않습니다.
// 우측 상단의 'Run this code' 버튼을 클릭하면 여러분이 직접 이 코드를 실행해볼 수 있습니다.
// 키보드 단축키는 'Ctrl + Enter'입니다.

// 이 코드는 자유롭게 수정할 수 있습니다. 마음대로 가지고 놀아보세요!
// 우측 상단의 'Undo Changes' 버튼을 클릭하면 원래 코드로 되돌릴 수 있습니다.

// 메인 함수입니다.
fn main() {
    // 컴파일된 바이너리가 호출될 때 이곳에 작성된 구문이 실행됩니다.

    // 콘솔에 텍스트를 출력합니다.
    println!("Hello World!");
}
```

`println!`는 콘솔에 텍스트를 출력하는
[**매크로**][macros]입니다.

프로그램 바이너리는 러스트 컴파일러(`rustc`)로 생성할 수 있습니다.

```bash
$ rustc hello.rs
```

`rustc` 명령어는 실행 가능한 `hello` 바이너리를 생성합니다.

```bash
$ ./hello
Hello World!
```

### 실습

실행 버튼을 클릭하면 어떤 결과가 나오는지 살펴보셨나요?
`println!` 매크로 한 줄을 새로 추가해 다음 결과가 나오도록
만들어보세요!

```text
Hello World!
I'm a Rustacean!
```

[macros]: macros.md

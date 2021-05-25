# use

`use` 구문으로 매번 스코프를 지정할 필요 없도록 만들 수 있습니다.

```rust,editable
// 사용하지 않은 코드(unused code) 경고를 숨기기 위한 속성입니다.
#![allow(dead_code)]

enum Status {
    Rich,
    Poor,
}

enum Work {
    Civilian,
    Soldier,
}

fn main() {
    // `use`를 명시하여, 스코프를 지정하지 않아도 되도록 만듭니다. 
    use crate::Status::{Poor, Rich};
    // `Work` 내 모든 이름을 `use` 합니다.
    use crate::Work::*;

    // `Status::Poor`과 동일합니다.
    let status = Poor;
    // `Work::Civilian`과 동일합니다.
    let work = Civilian;

    match status {
        // 앞서 `use`를 명시했으므로 스코프 지정은 불필요합니다.
        Rich => println!("부자는 돈이 많습니다!"),
        Poor => println!("빈민은 돈이 없습니다..."),
    }

    match work {
        // 마찬가지로 스코프 지정은 불필요합니다.
        Civilian => println!("시민이 일합니다!"),
        Soldier  => println!("군인이 전투합니다!"),
    }
}
```

### See also:

[`match`][match], [`use`][use] 

[use]: ../../mod/use.md
[match]: ../../flow_control/match.md

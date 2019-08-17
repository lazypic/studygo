# 인수

대부분의 프로그램은 사용자에게 입력을 받아서 무언가를 처리합니다.
인수를 처리하는 방법을 배워봅니다.

#### os.Args

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    var s, sep string
    for i := 1; 1 < len(os.Args); i++ {
        s += sep + os.Args[i]
        sep = " "
    }
    fmt.Println(s)
}
```

#### flag
일반적으로 소프트웨어를 개발할 때는 flag 라이브러리를 사용합니다.

> 참고: 러스콕스의 flag 예제코드 https://github.com/rsc/2fa/blob/master/main.go

```go
package main

import (
    "flag"
    "fmt"
)

var (
    flagAdd = flag.Bool("add", false, "add mode")
    flagDate = flag.String("date", "", "date string")
)

func main() {
    flag.Parse()
    fmt.Println(*flagAdd)
    fmt.Println(*flagDate)
}
```

#### 옵션을 만든는 방법
- 하나의 옵션에 여러값을 설정하는 형태가 되도록 작성하지 않는다.
- 인수는 Key, 값은 Value라고 생각하고 작성한다.
- Key와 Value로 항상 고유의 그래프를 그릴 수 있는 느낌으로 인수를 설계한다.

![graph_argv](./figures/graph_argv.png)

#### 실습

kalena 자료구조를 선언하고 flag 값을 설정해보는 예제 작성하기.
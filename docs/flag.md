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
규모가 있는 프로그램을 작성할 때는 flag를 설정합니다.

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

kalena 자료구조를 선언하고 flag 값을 설정해보는 예제 작성하기.
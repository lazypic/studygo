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
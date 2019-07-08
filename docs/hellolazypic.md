# Hello Lazypic

### Hello, lazypic
첫 코드는 Hello Lazypic을 출력해보는 시간입니다.
요즘 프로그래밍은 다국어를 지원하는 상황이 많이 발생하기도 합니다.
영어, 한글, 한자를 출력하겠습니다.

hellolazypic.go
```go
package main

import (
    "fmt"
)

func main() {
    fmt.Println("Hello, lazypic")
    fmt.Println("Hello, 레이지픽")
    fmt.Println("Hello, 來利之被")
}
```

Go는 기본적으로 UTF-8을 지원합니다. 여러 언어를 이용해서 코드를 작성할 때 아무것도 할 필요가 없습니다.

### 코드 실행
코드를 실행하는 방법은 간단합니다. `run` 명령어를 사용합니다.

```bash
$ go run hellolazypic.go
```
우리가 원한 결과가 잘 실행됩니다. 또한 go run을 실행하면 보이지 않았던, `go.mod` 파일이 생성됩니다.
go.mod (Go Module) 파일은 패키지, 의존성을 관리하기 위해 go에서 사용하는 의존성 관리시스템 입니다.
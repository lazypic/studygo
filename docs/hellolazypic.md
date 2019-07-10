# Hello Lazypic

### Hello, lazypic
첫 코드는 Hello, Lazypic을 출력해보는 시간입니다.
Go는 유니코드를 직접 처리합니다. 전 세계의 언어로 작성된 텍스트를 처리할 수 있습니다.

hellolazypic.go
```go
package main

import (
    "fmt"
)

func main() {
    fmt.Println("Hello, Lazypic")
    fmt.Println("Hello, 레이지픽")
    fmt.Println("Hello, 來利之被")
}
```

Go언어는 수많은 라이브러리가 있고 라이브러라는 package 이름으로 관리됩니다.
package에 main 이라고 작성되어 있는것은 독립된 실행 프로그램을 의미합니다.

import 는 우리가 사용하는 코드에 사용된 패키지명을 알려주는 역할을 합니다.
우리는 fmt 패키지 내부에 Println 함수를 사용하기 때문에 import에 fmt 패키지명을 작성했습니다.


### 코드 실행
코드를 실행하는 방법은 간단합니다. `run` 명령어를 사용합니다.

```bash
$ go run hellolazypic.go
```
우리가 원했던 결과가 터미널에서 잘 실행되는지 확인해주세요. 또한 go run을 실행하면 보이지 않았던, `go.mod` 파일이 생성됩니다.
go.mod (Go Module) 파일은 패키지, 의존성을 관리하기 위해 go에서 사용하는 파일입니다.
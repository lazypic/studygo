# Regular Expression / 정규식

인수를 통해서 사용자로 부터 받은 값의 형태가 소프트웨어 설계자가 의도한 값인지 쉽게 체크할 수 있는 방법으로는 일단 레귤러 익스프레션이 있습니다.

스터디로 진행중인 [kalena](https://github.com/lazypic/kalena) 프로젝트에 앞으로 자주 사용하게될 레귤러 익스프레션 형태를 예제코드로 작성해 보겠습니다.

# 시간과 관련된 정규식
`2019-08-01` 형태의 문자열인지 체크하는 레귤러 익스프레션을 작성해보겠습니다.

```go
package main

import (
    "regexp"
    "fmt"
)

func main() {
    var regexTime = regexp.MustCompile(`^\d{4}-(0?[1-9]|1[012])-(0?[1-9]|[12][0-9]|3[01])$`)
    t := "2019-08-20"
    if regexTime.MatchString(t) {
        fmt.Println("2019-08-01 형식의 문자열 입니다.")
    }
}
```

`2019-08-01T07:40:10` 또는 `2019-08-01 07:40:10` 형태의 문자열인지 체크하는 레귤러 익스프레션 작성해보기

참고자료: https://github.com/digital-idea/ditime

# 색상과 관련된 정규식
웹 컬러에 해당하는 `#FF0011` 형태의 문자인지 체크하는 레귤러 익스프레션을 작성해보겠습니다.

> 참고: 웹에서 사용하는 컬러는 대문자,소문서,3자리 같은 `#ff0011`, `#F01`, `#f01` 형식을 취할 수 있습니다.

```go
package main

import (
    "regexp"
    "fmt"
)

func main() {
    var regexWebColor = regexp.MustCompile(`^#([A-Fa-f0-9]{6}|[A-Fa-f0-9]{3})$`)
    c := "#FF00000"
    if regexTime.MatchString(t) {
        fmt.Println("2019-08-01 형식의 문자열 입니다.")
    }
}
```
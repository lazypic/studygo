# Test code
이번시간에는 함수를 하나 만들고 함수를 테스트할 수 있는 테스트 코드를 작성해보겠습니다.
클라우드 컴퓨터는 대부분 UTC 시간을 사용합니다.
우리는 한국에 있기 때문에 지역을 한국으로 설정하고 한국시간과 UTC 시간을 출력해보겠습니다.

```go
package main

import (
	"time"
	"log"
	"fmt"
	)

func main() {
	start := "2019-09-13T22:04:32"
	end := "2019-09-14T22:04:32"
	loc, err := time.LoadLocation("Asia/Seoul")
	if err != nil {
		log.Fatal(err)
	}
	s, err := time.Parse("2006-01-02T15:04:05", start)
	if err != nil {
		log.Fatal(err)
	}
	e, err := time.Parse("2006-01-02T15:04:05", end)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(s.In(loc))
	fmt.Println(s.UTC())
	fmt.Println(e.In(loc))
	fmt.Println(e.UTC())
}
```


start, end 시간을 두개 받아서 end 시간이 start 시간보다 미래의 시간인지 체크하는 함수 입니다.

check.go
```go
package main
import (
	"time"
)

func checkTime(start, end time.Time) bool {
    return end.After(start)
}
```

checkTime 함수가 들어간 상태로 다시 코드를 작성하겠습니다.
```go
package main

import (
	"time"
	"log"
	"fmt"
	)

func main() {
	start := "2019-09-15T22:04:32"
	end := "2019-09-14T22:04:32"
	loc, err := time.LoadLocation("Asia/Seoul")
	if err != nil {
		log.Fatal(err)
	}
	s, err := time.Parse("2006-01-02T15:04:05", start)
	if err != nil {
		log.Fatal(err)
	}
	e, err := time.Parse("2006-01-02T15:04:05", end)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(s.In(loc))
	fmt.Println(s.UTC())
	fmt.Println(e.In(loc))
	fmt.Println(e.UTC())
	fmt.Println(checkTime(s,e))
}

```

- reference time layout: https://yourbasic.org/golang/format-parse-string-time-date-example/
- UTC가 보안에 중요한 이유: http://www.itworld.co.kr/print/121140


### 테스트코드 작성
실제로 작성된 checkTime 함수가 논리적으로 잘 작동하는지 체크합니다.

check_test.go
```go
package main
import (
	"time"
	"testing"
)

func Test_checkTime(t *testing.T) {
    cases := []struct {
        start string
        end string
        want bool
    }{{
        start: "2019-09-13T22:04:32",
        end: "2019-09-14T22:04:32",
        want: true,
    }, {
        start: "2019-09-15T22:04:32",
        end: "2019-09-14T22:04:32",
		want: false,
	}, {
        start: "2019-09-15T22:04:32",
        end: "2019-09-15T22:04:33",
        want: true,
    }}
    loc, err := time.LoadLocation("Asia/Seoul")
    if err != nil {
        t.Fatal(err)
    }

    for _, c := range cases {
     	s, err := time.Parse("2006-01-02T15:04:05", c.start)
    	if err != nil {
	    	t.Fatal(err)
	    }
	    e, err := time.Parse("2006-01-02T15:04:05", c.end)
	    if err != nil {
		    t.Fatal(err)
	    }
		result := checkTime(s.In(loc), e.In(loc))
		if result != c.want {
			t.Fatalf("Test_checkTime(%s,%s): 얻은 값: %v, 원하는 값: %v", c.start, c.end, result, c.want)
		}
    }
}
```
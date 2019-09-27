# Test code
우리는 전 세계를 대상으로 특정 서비스를 만들 때 시간에 대해 고민할 필요가 있습니다.

클라우드 컴퓨터는 대부분 UTC 시간을 사용합니다.
이번 시간에는 시간과 관련된 함수 하나를 만들고, 만든 함수에 대한 테스트 코드를 작성해보겠습니다.
- 우리는 한국에 있기 때문에 지역을 한국으로 설정하고 한국시간과 UTC 시간을 출력해 보겠습니다.
- 우리와 한 시간의 오차가 있는 북경시간을 예외로 넣고 테스트해 보겠습니다.

```go
package main

import (
	"time"
	"log"
	"fmt"
	)

func main() {
	start := "2019-09-13T22:04:32+09:00"
	end := "2019-09-14T22:04:32+09:00"
	location := "Asia/Seoul"
	loc, err := time.LoadLocation(location)
	if err != nil {
		log.Fatal(err)
	}
	s, err := time.Parse("2006-01-02T15:04:05-07:00", start)
	if err != nil {
		log.Fatal(err)
	}
	e, err := time.Parse("2006-01-02T15:04:05-07:00", end)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(location, "start", s.In(loc))
	fmt.Println("UTC", "start", s.UTC())
	fmt.Println(location, "end", e.In(loc))
	fmt.Println("UTC", "end", e.UTC())
}
```
start 변수값을 중국/북경 시각인 `2019-09-13T22:04:32+08:00` 값으로 바꾸더라도 잘 변환되는것도 테스트해 보세요.

start, end 시간을 두 개 받아서 end 시간이 start 시간보다 미래의 시간인지 체크하는 함수입니다.

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
	start := "2019-09-15T22:04:32+09:00"
	end := "2019-09-14T22:04:32+09:00"
	loc, err := time.LoadLocation("Asia/Seoul")
	if err != nil {
		log.Fatal(err)
	}
	s, err := time.Parse("2006-01-02T15:04:05-07:00", start)
	if err != nil {
		log.Fatal(err)
	}
	e, err := time.Parse("2006-01-02T15:04:05-07:00", end)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(location, "start", s.In(loc))
	fmt.Println("UTC", "start", s.UTC())
	fmt.Println(location, "end", e.In(loc))
	fmt.Println("UTC", "end", e.UTC())
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
		startLocation string
		endLocation string
        want bool
    }{{
        start: "2019-09-13T22:04:32+09:00",
		end: "2019-09-14T22:04:32+09:00",
		startLocation: "Asia/Seoul",
		endLocation: "Asia/Seoul",
        want: true,
    }, {
        start: "2019-09-15T22:04:32+09:00",
		end: "2019-09-14T22:04:32+09:00",
		startLocation: "Asia/Seoul",
		endLocation: "Asia/Seoul",
		want: false,
	}, {
        start: "2019-09-15T21:04:31+08:00", // 중국시간
		end: "2019-09-15T22:04:32+09:00",
		startLocation: "Asia/Seoul",
		endLocation: "Asia/Seoul",
		want: true,
	}, {
        start: "2019-09-15T22:04:32+09:00",
		end: "2019-09-15T22:04:33+09:00",
		startLocation: "Asia/Seoul",
		endLocation: "Asia/Seoul",
        want: true,
    }}

    for _, c := range cases {
     	s, err := time.Parse("2006-01-02T15:04:05-07:00", c.start)
    	if err != nil {
	    	t.Fatal(err)
	    }
	    e, err := time.Parse("2006-01-02T15:04:05-07:00", c.end)
	    if err != nil {
		    t.Fatal(err)
		}
		startLoc, err := time.LoadLocation(c.startLocation)
		if err != nil {
			t.Fatal(err)
		}
		endLoc, err := time.LoadLocation(c.endLocation)
		if err != nil {
			t.Fatal(err)
		}
		result := checkTime(s.In(startLoc), e.In(endLoc))
		if result != c.want {
			t.Fatalf("Test_checkTime(%s,%s): 얻은 값: %v, 원하는 값: %v\n", s.In(startLoc).UTC(), e.In(endLoc).UTC(), result, c.want)
		}
    }
}
```

### Test 실행

터미널에서 다음처럼 타이핑하여 테스트를 실행합니다.

```
$ go test
```

- `go test`가 체크해주는 것
    - 코드 밴치마크
	- 테스트 코드 실행
	- 보고(레포트)
	- Coverage 체크
	- 레이스 상태 체크: https://blog.golang.org/race-detector
	    - 레이스 상태 참고자료: https://m.blog.naver.com/PostView.nhn?blogId=dev4unet&logNo=120055397425&proxyReferer=https%3A%2F%2Fwww.google.com%2F

#### Coverage체크시 count, atomic 차이
count: 코드 구분이 몇번이나 실행되는지 체크
atomic: 기본적으로 count와 같습니다. 다중 스레드 테스트에서 카운트 합니다. 좀더 오래 걸립니다.
```
$ go test -covermode=atomic
```

#### Go vet
`go vet`이 체크해주는 것: https://golang.org/cmd/vet/

# Method

자료구조를 작성했다면, 자료구조와 관련된 메소드도 같은 코드에 있는 것이 좋습니다.
효율적인 메소드는 코드의 가독성을 좋게하며, 코드가 짧아집니다.
kalena 를 제작하면서 필요한 에러체크 메소드를 예제로 생성해 보겠습니다.

```go
package main

import (
	"errors"
	"time"
)


// Schedule 자료구조
type Schedule struct {
	Title string
	Start string
	End   string
}

// CheckError 매소드는 Schedule 자료구조에 에러가 있는지 체크한다.
func (s Schedule) CheckError() error {
	if s.Title == "" {
		return errors.New("Title 이 빈 문자열 입니다")
	}
	if s.Start == "" {
		return errors.New("Start 시간이 빈 문자열 입니다")
	}
	if s.End == "" {
		return errors.New("End 시간이 빈 문자열 입니다")
	}
	
	startTime, err := time.Parse("2006-01-02T15:04:05-07:00", s.Start)
	if err != nil {
		return err
	}
	endTime, err := time.Parse("2006-01-02T15:04:05-07:00", s.End)
	if err != nil {
		return err
	}
	// end가 start 시간보다 큰지 체크하는 부분
	if !(endTime.After(startTime)) {
		return errors.New("끝시간이 시작시간보다 작습니다")
	}
	return nil
}
```
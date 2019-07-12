# collaboration

Go 언어를 이용해서 협업한다면, 아래 명령어 3개를 꼭 타이핑해주세요.

### gofmt

터미널에서 gofmt 를 타이핑하면 .go 파일을 자동으로 포멧팅합니다.

```bash
$ gofmt -w *.go
```

### go test
.go 파일을 테스트, 유닛테스트하는 명령어

```bash
$ go test
```

### go vet
.go 소스파일 검사, 인수검사, 문자열 형식과 Printf 호출 체크

```bash
$ go vet
```
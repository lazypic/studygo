# Build
단순하게 만들었던 우리의 hellolazypic.go 파일을 컴파일 해보겠습니다.

### go build
go 파일을 실행파일로 컴파일하는 방법입니다.

같은경로에 폴더 이름으로 실행파일이 생성됩니다.
```bash
$ go build
```

같은경로에 파일명으로 실행파일 생성됩니다.
```bash
$ go build hellolazypic.go
```


### Cross platform compile
동시에 맥, 리눅스, 윈도우즈 64비트용 실행파일을 컴파일 해보겠습니다.

```bash
GOOS=darwin GOARCH=amd64 go build -o ./bin/darwin/hellolazypic hellolazypic.go
GOOS=linux GOARCH=amd64 go build -o ./bin/linux/hellolazypic hellolazypic.go
GOOS=windows GOARCH=amd64 go build -o ./bin/windows/hellolazypic.exe hellolazypic.go
```

bash script로 만들면 빌드를 자동화 할 수 있습니다.
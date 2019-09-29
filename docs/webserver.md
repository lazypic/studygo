# Web Server
이번 시간에는 웹서버를 만들어 보겠습니다.

### 웹서버 생성
Go에서 웹서버를 생성하는 것은 간단합니다. "/" 주소 `:8080` 포트로 접근했을 때 hello world 메시지가 보이는 코드는 아래와 같습니다.

```go
http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("hello world"))
})
http.ListenAndServe(":8080", nil)
```

### 웹서버 리펙토링

앞으로 서비스가 확장되며 수많은 페이지를 생성해야 합니다.
http.go 파일을 생성하고 웹과 관련된 코드는 http.go 파일에 선언합시다.


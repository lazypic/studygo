# restAPI

### POST
데이터를 넣을 때 사용합니다.

### GET
데이터를 가지고 올 때 사용합니다.

### PUT
데이터를 수정할 때 사용합니다.

### DELETE
데이터를 삭제할 때 사용합니다.


### OPTIONS
현재 End-point가 제공 가능한 API method를 반환하도록 짜줍니다.

```
HTTP/1.1 200 OK
Allow: GET,PUT,DELETE,OPTIONS,HEAD
```


### HEAD
요청을 했을 때 Header만 반환합니다.

### PATCH
특정 값만 바꾸고 싶을 때 사용합니다.
PUT과 구분해서 사용하는 추세입니다.
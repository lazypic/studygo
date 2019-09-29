# mongoDB for Golang
Go에서 mongoDB를 사용하기 위해서 사용하는 라이브러리를 다룹니다.

대표적인 라이브러로는 [mongo-go-driver](https://github.com/mongodb/mongo-go-driver)와 [mgo](https://github.com/globalsign/mgo)가 있습니다.

만들어지기는 mgo가 먼저 만들어졌지만 mongodb측에서 공식적으로 mongo-go-driver를 지원하며 mongo-go-driver를 사용하는 추세로 바뀌고 있습니다.

> MongoDB has released an official driver for the Go language that is appropriate for all supported database operations. This driver implements the Core and API specs, and supports MongoDB 3.2 and above. 발췌: https://www.mongodb.com/blog/post/go-migration-guide

mongo-go-driver를 다루기 위해서는 다음 조건이 필요합니다.
- Go 1.10 이상
- MongoDB 2.6 이상

#### 설치

```bash
$ go get go.mongodb.org/mongo-driver
```

#### 라이브라리 사용

```go
import (
    "context"
    
    "go.mongodb.org/mongo-driver/bson"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)
```

#### Reference
- https://www.mongodb.com/blog/post/mongodb-go-driver-tutorial
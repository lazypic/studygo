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

#### mongoDB의 특징
대부분의 RDBMS는 Row단위로 Lock을 지원합니다.
mongoDB는 데이터베이스 단위의 Lock을 지원합니다.
기존 RDBMS 사용자는 데이터 무결성에 이해할 수 없는 방식이라고 생각합니다.
또한 mongoDB는 데이터베이스별로 ReadLock, WriteLock이 있습니다. ReadLock은 여러개의 Operation에서 공유가 가능하지만 WriteLock은 하나만 사용할 수 있습니다. WriteLock은 항상 ReadLock보다 우선권을 가지고 있습니다.
말하자면 mongoDB에서 동시에 Read,Write 작업이 대기하고 있다면 항상 Write 작업이 먼저 실행됩니다.
따라서 mongoDB에서 동시에 데이터를 넣으면 작업을 수행하지 못하게 됩니다. 한번에 여러 데이터를 넣지 말아주세요.

> 참고: https://docs.mongodb.com/manual/faq/concurrency/

#### 데이터 추가
```go
import (
    "context"
    "go.mongodb.org/mongo-driver/bson"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)

ctx, _ := context.WithTimeout(context.Background(), 5*time.Second)
client, err := mongo.Connect(ctx, options.Client().ApplyURI("mongodb://localhost:27017"))
if err != nil {
    log.Println(err)
}
collection := client.Database("kelena").Collection("user1")
res, err := collection.InsertOne(ctx, bson.M{"title": "to do", "layer": "family"})
if err != nil {
    log.Println(err)
}
id := res.InsertedID
```

#### 데이터 검색

```go
import (
    "context"
    "go.mongodb.org/mongo-driver/bson"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)

var result struct {
    Title string
    Layer string
}

filter := bson.M{"title": "to do"}
ctx, _ = context.WithTimeout(context.Background(), 5*time.Second)
client, err := mongo.Connect(ctx, options.Client().ApplyURI("mongodb://localhost:27017"))
if err != nil {
    log.Println(err)
}
col := client.Database("kelena").Collection("user1")
err = col.FindOne(ctx, filter).Decode(&result)
if err != nil {
    log.Fatal(err)
}
```

#### 데이터 삭제

```go
import (
    "context"
    "go.mongodb.org/mongo-driver/bson"
    "go.mongodb.org/mongo-driver/mongo"
    "go.mongodb.org/mongo-driver/mongo/options"
)

ctx, _ = context.WithTimeout(context.Background(), 5*time.Second)
client, err := mongo.Connect(ctx, options.Client().ApplyURI("mongodb://localhost:27017"))
if err != nil {
    log.Println(err)
}
col := client.Database("kelena").Collection("user1")
res, err := col.DeleteOne(ctx, bson.M{"title": "to do"})
if err != nil {
    log.Fatal("DeleteOne() ERROR:", err)
}
fmt.Println("DeleteOne Result TYPE:", reflect.TypeOf(res))
```

#### Reference
- https://www.mongodb.com/blog/post/mongodb-go-driver-tutorial
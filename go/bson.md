# BSON

- json의 바이너리 인코딩 형태
- MongoDB의 document가 bson형태로 저장됨
- 신뢰도 높은 process, sort, compare data 작업 가능

## 형태

### D

- BSON Document
- document를 쿼리할 때 사용하며 순서가 존재한다

### M

- An unorderd Map
- D와 같지만 순서가 없다

### A

- BSON Array
- D안에 배열로 존재하는 element이다

### E

- Single element
- D or A안에 있는 하나의 element이다

## 사용

Create

```go
    insertResult, _ := uesrsCollection.InsertOne(context.TODO(), bson.D{
		primitive.E{Key: "userID", Value: "test1234"},
		primitive.E{Key: "array", Value: bson.A{"flying", "squirrel", "dev"}},
	    })
```

READ

```go
    readFilter := bson.D{
        primitive.E{Key: "userID", Value: "test1234"},
    }

    // One
    var result []bson.M
    err = collection.FindOne(context.TODO(), readFilter).DECODE(&result)

    // All
    cursor, err := uesrsCollection.Find(context.TODO(), bson.D{{}})
	if err != nil {
		fmt.Println("에러!")
		fmt.Println(err)
	}
	for cursor.Next(context.TODO()) {
		var elem bson.M
		err := cursor.Decode(&elem)

		if err != nil {
			fmt.Println(err)
		}
		fmt.Println(elem)
	}
```

UPDATE

```go
	updateFilter := bson.D{
		primitive.E{Key: "userID", Value: "test1234"},
	}
	updateBson := bson.D{
		primitive.E{Key: "$push", Value: bson.D{
			primitive.E{Key: "array", Value: "wow"},
		},
		},
	}
```

DELETE

```go
	deleteFilter := bson.D{
		primitive.E{Key: "userID", Value: "test1234"},
	}
	deleteResult, _ := uesrsCollection.DeleteOne(
		context.TODO(),
		deleteFilter,
	)
```

# Goroutine

- 스케줄러에서 관리되는 OS스레드 보다 가벼운 자체 스레드
- 리소스 사용 면에서 효율적이며, channel을 통해 goroutine간 데이터 전송 가능

### OS스레드와 비교했을 때의 장점

- 비용이 적음 -> OS스레드: 약 1MB, goroutine: 수KB
- 여러개의 goroutine을 하나의 OS스레드에 매핑 가능
- channel을 통해 공유 메모리 접근 시 발생하는 문제 해결

### 사용

- go 키워드를 사용해서 실행가능

```go
go hello() // 함수앞에 go 키워드 선언

for i := 0; i < 3; i++ {// 익명함수(클로저)를 통해서도 가능
    go func(n int) {
        f.Println("goroutine : ", n)
        oneTime.Do(Hello)
    }(i)
}
```

#### 다중 고루틴 사용 ex)

```go
package main

import (
	"fmt"
	"time"
)

func sarc() {
	var cur = 0
	for i := 1; i <= 5; i++ {
		time.Sleep(100 * time.Millisecond)
		cur += 100
		fmt.Println("sarc", i, "current:", cur, "ms")
	}
}

func tech() {
	var cur = 0
	for i := 1; i <= 5; i++ {
		time.Sleep(150 * time.Millisecond)
		cur += 150
		fmt.Println("tech", i, "current:", cur, "ms")
	}
}

func main() {
	go sarc()
	go tech()
	time.Sleep(3 * time.Second)
	fmt.Println("Main has been terminated")
}
```

```
sarc 1 current: 100 ms
tech 1 current: 150 ms
sarc 2 current: 200 ms
tech 2 current: 300 ms
sarc 3 current: 300 ms
sarc 4 current: 400 ms
tech 3 current: 450 ms
sarc 5 current: 500 ms
tech 4 current: 600 ms
tech 5 current: 750 ms
Main has been terminated
```

- sarc는 100ms, tech는 150ms 단위로 실행
- main에서는 해당 goroutine들이 끝나는 시간을 기다림

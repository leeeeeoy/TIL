# Channel

- goroutine에서 정보를 주고받는 방식
- 공유 메모리 접근 문제를 해결하도록 설계되어 있음

## 사용법

채널생성

```go
// unbuffered 생성
channel := make(chan string)

// 10개의 buffer를 가진 channel생성
channel := make(chan string, 10)
```

- unbuffered와 buffered 생성 가능
- unbuffered channel의 경우, 수신자가 받을 때까지 대기
- buffered의 경우 공간이 남아있을 때, 값 복사 비용만큼 대기 -> 다른 작업(비동기) 가능

채널사용

```go
func main() {
    // string형 채널을 생성합니다.
    channel := make(chan string)

    // goroutines을 실행
    go func(str string) {
        // 전달 받은 변수를 수정해서 channel에 전달
        channel <- "My name is " + str
    }("Ahn")

    // channel을 통해서 데이터를 전달 받습니다.
    result := <-channel

    println(result)
}
```

- channel<- : 임의의 값을 channel로 전달, 즉 채널로 데이터를 보냄
- <-channel : channel을 통해 데이터 전달, 즉 채널로부터 데이터를 받음

송수신 채널 설정

```go
//OnlySendChannel 함수는 인자로 송신만 가능한 채널을 전달합니다.
func OnlySendChannel(ch chan<- string){
    // 채널에 string을 송신함
    ch <- "Only Send ch"
    // error 발생 ch에서 수신 못함!!
    <- ch
}
// OnlyRecvChannel 함수는 인자로 수신만 가능한 채널을 전달합니다.
func OnlyRecvChannel(ch <-chan string){
	// 채널에 string을 수신함
    value := <- ch
    println(value)

    // error 채널에 string을 송신 못함
    ch <- "receive complete"
}
```

- chan<- : 보내는 것만 가능한 채널 (채널로 데이터를 보내는 것만 가능)
- <-chan : 받는 것만 가능한 채널 (채널로부터 데이터를 받는 것만 가능)

### Select 문을 사용한 예시

```go
func main(){
    reqc := make(chan chan int)

    go func(reqc chan chan int) {
        for {
            select {
                case resc := <-reqc:
                    log.Println("another goroutine receives a request")
                    resc <- 42
            }
        }
    }(reqc)
    request := func() int {
        req := make(chan int)
        reqc <- req
        return <-req
    }
    log.Println("the main goroutine receives a response:", request())
}

```
